# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Allow usage in the Table Extension (`table:columns`)

## [1.0.0]

### Added

- Allow usage in Bands and the Data Cube Extension
- Add `cf:cell_methods`
- Explicitly list and allow `description` and `unit` to mirror their CF counter-parts

### Changed

### Deprecated

### Removed

- `cf:parameter`, use `cf:standard_name` instead

### Fixed

## [0.2.0]

### Changed

- `cf:parameter` can be used in Collections without having assets.

## [0.1.0]

- First release

[Unreleased]: <https://github.com/stac-extensions/cf/compare/v1.0.0...HEAD>
[1.0.0]: <https://github.com/stac-extensions/cf/compare/v0.2.0...1.0.0>
[0.2.0]: <https://github.com/stac-extensions/cf/compare/v0.1.0...0.2.0>
[0.1.0]: <https://github.com/stac-extensions/cf/tree/v0.1.0>
