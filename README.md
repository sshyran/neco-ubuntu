Ubuntu image customizer
=======================

This repository contains a Makefile to build a custom Ubuntu ISO installer
and a custom cloud image.  The cloud image are to be used with [placemat][]
and [placemat-menu][] to prepare network boot servers in a virtual data center.

Prerequisites
-------------

The Makefile assumes to run on a recent Ubuntu or Debian OS.
To test built images, QEMU/KVM is used.

Build
-----

1. Prepare `setup/cluster.json` file.

    The contents should be a JSON array of objects with these fields:

    | Name              | Type   | Description                              |
    | ----------------- | ------ | ---------------------------------------- |
    | `name`            | string | Cluster name                             |
    | `bastion_network` | string | IPv4 address of the bastion network      |
    | `bmc_network`     | CIDR   | IPv4 network address in CIDR for the BMC |
    | `ntp_servers`     | array  | List of NTP server addresses             |

    This file will be read by `setup-neco-network`.
    An example of the file is available at `setup/cluster.json.example`.

2. Run `make` to see available build options.
3. Run `make setup`.  This is a one-time procedure.
4. Run `make all` to build everything.

* `build/cybozu-ubuntu-18.04-server-amd64.iso` is the custom ISO installer.
* `build/cybozu-ubuntu-18.04-server-cloudimg-amd64.img` is the custom cloud image.

Test
----

Built images can be tested with `make preview-iso` and `make preview-cloud`.

They require a Linux host that can run QEMU/KVM.  If your host itself is a
virtual machine, you need to enable nested virtualization.
For Hyper-V, run the following command in *administrator's* PowerShell console
after shutting down the virtual machine.

```console
$ Set-VMProcessor -VMName <VMName> -ExposeVirtualizationExtensions $true
```

To run QEMU/KVM w/o root privileges, add `kvm` group to your account.
You need to logout and login to gain the group privilege.

```console
$ sudo adduser $USER kvm
$ exit
```

They also require X Window System.  [MobaXterm](https://mobaxterm.mobatek.net/)
is quite handy to run X on Windows.

Usage
-----

### Custom ISO installer

This installer is meant to setup a netboot service on a physical server.
Most installation options are preseeded; options need to be inputted manually are:

* Hostname
* Password for "cybozu" user.
* Storage partitioning
* Passphrase for LVM encryption.

### Custom cloud image

Use [cloud-init][] to configure your cloud instance.

### Setup after installation

1. Install `rkt`

    For cloud image installation, install `rkt` as follows.

    ```console
    $ cd /extras/setup
    $ sudo ./setup-rkt
    ```

2. Configure network

    Run `setup-neco-network` script as follows.
    This configures `systemd-networkd` for networking, `bird` for routing,
    and `chrony` for time adjustment.

    ```console
    $ cd /extas/setup
    $ sudo ./setup-neco-network RACK_NUMBER
    ```

### Notes

After setup, the system is configured as follows.

* Running `systemd-networkd` instead of `netplan.io`.  `netplan.io` is purged.
* Running `rkt` containers as systemd services.  Use `sudo rkt list` to get the list of them.
* The rack number of the server is stored in `/etc/neco/rack` file.
* The cluster ID of the server is stored in `/etc/neco/cluster` file.
* The IPAM configuration for sabakan is stored in `/etc/neco/sabakan_ipam.json` file.

License
-------

[MIT][]

[placemat]: https://github.com/cybozu-go/placemat
[placemat-menu]: https://github.com/cybozu-go/placemat-menu
[cloud-init]: https://cloudinit.readthedocs.io/
[sabakan]: https://github.com/cybozu-go/sabakan
[etcdpasswd]: https://github.com/cybozu-go/etcdpasswd
[MIT]: https://opensource.org/licenses/MIT
