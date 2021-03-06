# Change Log

All notable changes to this project will be documented in this file.

## [Unreleased]

## [20190829]

### Changed
- [setup-route] Reboot when setup-route.service is failed (#47).

## [20190607]

### Changed
- Adjust makestep offset for chrony to 0.1 seconds (#45).

## [20190528]

### Changed
- Purge unattended-upgrades (#41).

## [20190521]

### Changed
- Rebuild cloud image in the latest version

## [20190312]

### Changed
- Use internal ntp address by default (#39).

## [20190213]

### Changed
- add "node-gateway-offset" field to sabakan_ipam.json (#38).

## [20190131]

### Added
- Dump /etc/neco/sabakan_ipam.json (#37).

### Changed
- "bmc_network" field to cluster.json (#37).

### Removed
- serf ACI file.

## [20181010]

### Changed
- Update serf ACI file.

## [20181009]

### Added
- Add serf ACI file (#36).

## [20180926]

### Changed
- Ensure time synchronized (#35).

## [20180919]

### Added
- Disable network device offloading (#34).

## [20180906]

### Changed
- Rebuild image with latest container images.

## [20180817]

### Changed
- Mask `systemd-timesyncd.service` as it conflicts with chrony (#32).

## [20180814]

### Added
- First release of neco-ubuntu images (#31).

[Unreleased]: https://github.com/cybozu/neco-ubuntu/compare/20190829...HEAD
[20190829]: https://github.com/cybozu/neco-ubuntu/compare/20190607...20190829
[20190607]: https://github.com/cybozu/neco-ubuntu/compare/20190528...20190607
[20190528]: https://github.com/cybozu/neco-ubuntu/compare/20190521...20190528
[20190521]: https://github.com/cybozu/neco-ubuntu/compare/20190312...20190521
[20190312]: https://github.com/cybozu/neco-ubuntu/compare/20190213...20190312
[20190213]: https://github.com/cybozu/neco-ubuntu/compare/20190131...20190213
[20190131]: https://github.com/cybozu/neco-ubuntu/compare/20181010...20190131
[20181010]: https://github.com/cybozu/neco-ubuntu/compare/20181009...20181010
[20181009]: https://github.com/cybozu/neco-ubuntu/compare/20180919...20181009
[20180919]: https://github.com/cybozu/neco-ubuntu/compare/20180906...20180919
[20180906]: https://github.com/cybozu/neco-ubuntu/compare/20180817...20180906
[20180817]: https://github.com/cybozu/neco-ubuntu/compare/20180814...20180817
[20180814]: https://github.com/cybozu/neco-ubuntu/compare/946c82a...20180814
