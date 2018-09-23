# The assistive devices JSON schema

This document helps you to understand the structure of the [assistive devices JSON](https://github.com/mdn/browser-compat-data/tree/master/devices) files.

#### Browser identifiers

The currently accepted assistive devices identifiers are [defined in the a11y-compat-data schema](https://github.com/mdn/browser-compat-data/blob/master/schemas/a11y-compat-data-schema.md#browser-identifiers). They are re-used for the assistive devices data schema. No other identifiers are allowed and the file names should also use the assistive device identifiers.

For example, for the assiste device identifier `nvda`, the file name is `nvda.json`.

#### File structure

The file `nvda.json` is structured like this:

```json
{
  "devices": {
    "nvda": {
      "name": "NVDA",
      "releases": {
        "2018.1": {
          "release_date": "2018-03-2018",
          "release_notes": "https://www.nvaccess.org/files/nvda/releases/2018.1/nvda_2018.1_changes.html",
          "status": "retired"
        }
      }
    }
  }
}
```

It contains an object with the property `devices` which then contains an object with the browser identifier as the property name (`nvda`).

Underneath, there is a `releases` object which will hold the various releases of a given browser by their release version number (`"2018.1"`).

### `name`

The `name` string is an optional property which should use the browser brand name and avoid English words if possible, for example `"NVDA"`, `"JAWS"`, `"VoiceOVer"`, etc.

### Release objects
The release objects consist of the following properties:

* A mandatory `status` property indicating where in the lifetime cycle this release is in. It's an enum accepting these values:
  * `retired`: This release is no longer supported (EOL).
  * `current`: This release is the official latest release.
  * `exclusive`: This is an exclusive release (for example on a flagship device), not generally available.
  * `beta`: This release will the next official release.
  * `nightly`: This release is the current alpha / experimental release (like Firefox Nightly, Chrome Canary).
  * `esr`: This release is an Extended Support Release.
  * `planned`: This release is planned in the future.

* An optional `release_date` property with the `YYYY-MM-DD` release date of the browser's release.

* An optional `release_notes` property which points to release notes. It needs to be a valid URL.

### Exports

[NOT DONE YET]This structure is exported for consumers of `mdn-browser-compat-data`:

```js
> const compat = require('mdn-browser-compat-data');
> compat.devices.nvda.releases[''].status;
// "retired"
```
