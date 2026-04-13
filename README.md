# CF Extension Specification

- **Title:** CF
- **Identifier:** <https://stac-extensions.github.io/cf/v0.3.0/schema.json>
- **Field Name Prefix:** cf
- **Scope:** Item, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @Fred-Leclercq

This document explains the CF Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
It adds a field to provide the Standard Name Table based on the [CF metadata convention](http://cfconventions.org/).

- Examples:
  - [Item](examples/item.json) and [Collection](examples/collection.json):
    Shows the basic usage of the extension in a STAC Item and a corresponding summarizing STAC Collection
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [x] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [x] Bands
- [x] Data Cube Extension (`cube:variables`, `cube:dimensions`)
- [ ] Links

| Field Name       | Type      | Description |
| ---------------- | --------- | ----------- |
| cf:standard_name | string    | Corresponds to the [CF Standard Name](https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html). |
| cf:cell_methods  | \[string\|null] | A list of string or `null` attributes that describe the "method" applied to the data as defined in the CF conventions. |
| description      | string    | Corresponds to the [CF `long_name`](https://cfconventions.org/cf-conventions/cf-conventions.html#long-name). |
| unit             | string    | Corresponds to the [CF `units`](https://cfconventions.org/cf-conventions/cf-conventions.html#units). |

### Additional Field Information

#### cf:standard_name

The CF standard name is a controlled vocabulary term used in Climate and Forecast (CF) metadata conventions
to unambiguously describe the physical quantity represented by a variable in climate and geophysical data files.
If variable has a standard_name definition in the CF convention, it must be a non-empty value from the
[CF Standard Name Table](https://cfconventions.org/Data/cf-standard-names/current/build/cf-standard-name-table.html).
Otherwise `cf:standard_name` is an empty value.

#### cf:cell_methods

The cell_methods attribute in the CF (Climate and Forecast) convention is designed to describe how the values in a data variable
were derived with respect to one or more axes (e.g., time, latitude, longitude). Each "method" represents the statistical or
computational operations applied to data along specific axes. For example, if used within the datacube extension then the
order of cell_methods aligns with the order of spatial and temporal extensions.

```json
"cube:variables": {
  "some_variable": {
    "cf:cell_methods": [null, "minimum"],
    "dimensions": [
        "vertical_dimension1",
        "time_interval2"
    ]
  }
}
```

In this case `null` indicates that no method is applied over the first dimension `vertical_dimension1` but 
the `minimum` method is applied over the second dimension `time_interval2`. 
These dimensions would be defined in the `cube:dimensions` fields.

If a data value is representative of variation over a combination of axes this approach is not sufficient \(e.g. the standard
deviation of topographic height within a longitude-latitude gridbox would have `cell_methods="latitude: longitude: standard_deviation"`\).
Such `cell_methods` cannot be described as per dimension methods in an array and would need a plain string representation.

```json
"cube:variables": {
  "some_variable": {
    "cf:cell_methods": "latitude: longitude: standard_deviation",
    "dimensions": [
        "latitude",
        "longitude"
    ]
  }
}
```

See [CF Cell Methods](https://cfconventions.org/cf-conventions/cf-conventions.html#cell-methods) for more details.

#### description

The description field as defined by the [NUG](https://docs.unidata.ucar.edu/nug/current/index.html) is meant to contain a long descriptive 
name which may, for example, be used for labeling plots. 
See [CF "long_name"](https://cfconventions.org/cf-conventions/cf-conventions.html#long-name) for more details.

#### unit

The unit of measurement for the values, preferably compliant to [UCUM](https://ucum.org/[) (unit code)
or [UDUNITS-2](https://ncics.org/portfolio/other-resources/udunits2/) (unit symbol or alternatively singular unit name).
Unit is not required for dimensionless quantities. A variable with no unit attribute is assumed to be
dimensionless. The conforming unit for quantities that represent fractions, or parts of a whole, is "1".
Descriptive information about dimensionless quantities, such as sea-ice concentration, cloud fraction,
probability, etc., should be given in the "description" attribute rather than the unit field.
See [CF "units"](https://cfconventions.org/cf-conventions/cf-conventions.html#dimensionless-units) for more details.

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
