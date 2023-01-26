# Template Extension Specification

- **Title:** CF
- **Identifier:** <https://stac-extensions.github.io/cf/v1.0.0/schema.json>
- **Field Name Prefix:** cf
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @Fred-Leclercq

This document explains the Template Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
This is the place to add a short introduction.

- Examples:
  - [Item example](examples/item.json): Shows the basic usage of the extension in a STAC Item
  - [Collection example](examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Fields

The fields in the table below can be used in these parts of STAC documents:
- [ ] Catalogs
- [ ] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name           | Type                     | Description                         |
|----------------------|--------------------------|-------------------------------------|
| cf:parameter         | [CF Object](#CF-object) | **REQUIRED**. CF Standard Name Table |

### Additional Field Information
#### cf:parameter

The cf:parameter array is used to describe the parameters in an Asset. This enables clients to read
the file and understand which parameters are available. 

The cf:parameter array may optionally be used in the Item Properties to summarize the available parameters in the assets.
This should be a 'union' of all the possible parameters represented in assets. It should be considered merely informative - clients should rely on 
the cf:parameter of each asset.  
An Item is only allowed to use cf:parameter in its Properties if it has at least one asset with a defined parameter array.

#### CF Object

This object should contain a variable name from the [CF list](https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html) 
and where applicable a unit from the  [UDUNITS-2 database](https://docs.unidata.ucar.edu/udunits/current/)

| Field Name | Type   | Description                                                                                   |
|------------|--------|-----------------------------------------------------------------------------------------------|
| name       | string | **REQUIRED**. Should be a value from the CF standard names list                               |
| unit       | string | Indicates the unit, preferably available in the database from the UDUNITS-2 package (unidata) |

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:
```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:
```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:
```bash
npm run format-examples
```
