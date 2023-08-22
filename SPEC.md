# The GP_Vendors database spec

## Structure

The GP_Vendors database is stored as a basic text file, with a bit of "formatting".

It is mainly split up into 3 different things:
- Meta tags
- Comments
- Data indices

The database should feature meta tags at the beginning, followed by a mix of data and comments.

### Meta tags

The meta tags are prepended with a ".", followed by 2 whitespace seperated values, the key and value.  
For certains keys there can be multiple values, which is achieved by simply writing the meta tag multiple times.

### Comments

Comments are single-line pieces of texts prepended with `#$`. Any line starting with `#$` should be ignored by the database parser(or at least not treated as data)

### Data indices

Data indices are the most complex, and will be elaborated on further down. A short brief could be that:
- They're not prefixed with anything
- They contain a string of data seperated by semicolons(`;`)
- They are single-line

## Valid meta tags
Any tag that is valid since a newer version than the newest specified in the document should be ignored.  

All version tags should be the first thing in the document.

The `Valid Since` field follows the `Valid Since` spec lower down in the document

| Name | Description | Valid Since |
| ---- | ----------- | ----------- |
| version | Specifies a version of GP_Vendors being used | 1.0 |
| vendor | Specifies that a certain vendor is potentially used | 1.0 |
| mapping | Specifies that a certain mapping is potentially used | 1.0 |
| extension | Specifies that a certain extension | 1.0 |
| experimental | Specifies that the file contains experimental stuff(unregistered extensions etc) | 1.0 |

## Extensions
Extensions are a feature of this database that could be seen as over-engineered, and it probably is, but the core idea is that:
- If you have a database you want to publicise, and you want to store more data than allowed in the spec, you can just write an extension and it will be fully valid.
Registration of extensions can be done by opening a PR with a file in the EXT directory of the GP_Vendors repository.

Extensions should be named like they are in OpenGL, `EXT_[creator]_ID`, where [creator] is the group behind the extension

## Data indices
Data indices are specified as a single-line string, with the different parts seperated by semicolons(`;`).

When `index` is referred to, the "row" is meant. That is, the piece of data that ends with the newline.
When `piece` is referred to, the "column" is meant. That is, the piece of data that is seperated with semicolons.

If an index is of a version newer than supported by a piece, that piece should be skipped.
If a piece is newer than the index, that piece should be skipped.

If a piece is skipped, it should default to the default value.

If a piece is marked with `?` it is unknown, and it should resort to using the default value.

Any default value marked with `REQUIRED` is part of 1.0, and is mandatory meta data.

The `Valid Since` field follows the `Valid Since` spec lower down in the document

| Name | Description | Valid Since | Default Value |
| - | - | - | - |
| Version | The version of the index | 1.0 | REQUIRED |
| UUID | The UUID of the gamepad | 1.0 | Whatever NULL UUID suits your needs |
| Name | The name of the gamepad | 1.0 | An empty string |
| Mapping | The mapping of the gamepad, see `Mappings` | 1.0 | `unknown` |
| Vendor | The producer of the gamepad, see `Vendors` | 1.0 | An empty string |

## "Valid Since" specification

Valid Since fields can be written in a couple ways.
- Just a version - This means "anything equal to or above"
- `A`-`B` - This means "anything between version A and version B, including A and B"
- `A`-`B`, `C`-`D` - This means "anything between A and B, or C and D, including A, B, C and D". Can be more than 2 pairs
- !`A` - This means "only in version A", and should be treated as experimental.

## Mappings
There are a number of valid mappings that can be used.

This list only contains official ones.

Additional mappings can be used freely, and can be handled as `unknown` if you don't support them.

| Name | Description | Valid Since |
| - | - | - |
| `xbox` | A generic Xbox one-style controller | 1.0 |
| `xbox360` | A generic Xbox 360-style controller | 1.0 |
| `ps3` | A generic PS3-style controller(includes PSX and PS2) | 1.0 |
| `ps4` | A generic PS4-style controller | 1.0 |
| `switch` | A generic Nintendo Switch-style controller | 1.0 |

## Vendors
There are a number of valid vendors that can be used.

This list only contains official ones.

Additional vendors can be used freely, and can be handled as `unknown` if you don't support them.

| Name | Description | Valid Since |
| - | - | - |
| `microsoft` | N/A | 1.0 |
| `sony` | N/A | 1.0 |
| `nintendo` | N/A | 1.0 |
| `8bitdo` | N/A | 1.0 |
