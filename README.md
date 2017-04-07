# Contentful import tool

[![npm](https://img.shields.io/npm/v/contentful-import.svg)](https://www.npmjs.com/package/contentful-import) [![Build Status](https://travis-ci.org/contentful/contentful-import.svg?branch=master)](https://travis-ci.org/contentful/contentful-import) [![Coverage Status](https://coveralls.io/repos/github/contentful/contentful-import/badge.svg?branch=master)](https://coveralls.io/github/contentful/contentful-import?branch=master) [![Dependency Status](https://img.shields.io/david/contentful/contentful-import.svg)](https://david-dm.org/contentful/contentful-import) [![devDependency Status](https://img.shields.io/david/dev/contentful/contentful-import.svg)](https://david-dm.org/contentful/contentful-import#info=devDependencies)

[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release) [![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

[https://www.contentful.com](Contentful) is a content management platform for web applications, mobile apps and connected devices. It allows you to create, edit & manage content in the cloud and publish it anywhere via powerful API. Contentful offers tools for managing editorial teams and enabling cooperation between organizations.

This Command Line Tool (CLI) helps you to import files generated by the [contentful-export](https://github.com/contentful/contentful-export) tool to new and empty Contentful spaces.

## Installation

We recommend you install the CLI via npm:

```bash
npm install -g contentful-import
```

## Usage and examples

```
Usage: contentful-import [options]

Options:
  --version                  Show version number                       [boolean]

  --space-id                 ID of the destination space     [string] [required]

  --management-token         Contentful management API token for the destination
                             space                           [string] [required]

  --content-file             JSON file that contains data to be import to your
                             space                           [string] [required]

  --content-model-only       Import only content types[boolean] [default: false]

  --skip-content-model       Skip importing content types and locales
                                                      [boolean] [default: false]

  --skip-locales             Skip importing locales   [boolean] [default: false]

  --skip-content-publishing  Skips content publishing. Creates content but does
                             not publish it           [boolean] [default: false]

  --error-log-file           Full path to the error log file            [string]

  --config                   An optional configuration JSON file containing all
                             the options for a single run
```

### Example

```shell
contentful-import \
  --space-id spaceID \
  --management-token managementToken \
  --content-file exported-file.json \
```

or

```shell
contentful-import --config example-config.json
```

You can create your own configuration file based on the [_example-config.json_](example-config.json) file.

### Usage as a library

While this tool is intended for use as a command line tool, you can also use it as a Node library:

```javascript
let spaceImport = require('contentful-import')
let options = {
    content: {entries:..., contentTypes:..., locales:...},
    spaceId: 'SPACE_ID',
    managementToken: 'MANAGEMENT_TOKEN'
}
spaceImport(options)
.then((output) => {
  console.log('Data Imported successfully')
})
.catch((err) => {
  console.log('oh no! errors occurred!', err)
})
```

The `options` object can contain any of the CLI options, but written with a camelCase pattern instead and no dashes. For example `--space-id` would become `spaceId`.

## Limitations

- This tool currently does **not** support the import of space memberships.
- Imported webhooks with credentials will be imported as normal webhooks. Credentials should be added manually afterwards.
- If you have custom UI extensions, you need to reinstall them manually in the new space.

## Changelog

Read the [releases](https://github.com/contentful/contentful-import/releases) page for more information.

## License

This project is licensed under MIT license

[1]: https://www.contentful.com
