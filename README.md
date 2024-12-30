# Malla API Data

Transcriptions of the official major mallas of Facultdad de Ciencias Físicas y Matemáticas of Universidad de Chile.

[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg

## Data Structure

The macro-order in this repository is as follows:

```
Faculty Name
\=> API Version
   \=> Mallas Directory
   \=> Templates Directory
   \=> Extended Attributes File
```

> [!WARNING]
> As of `v0` the API supports *vertical groups* for courses, called degrees and aligned with the semesters.
>
> However, it **does not** support *horizontal groups* for courses, commonly called lines.
>
> This complexity must be addressed inside the [Extended Attributes](./EXTENDED_ATTR) **and not** inside the course block.

### API Version

> Starts from `v0`.

The following **will not happen**:

1. Keys getting renamed.
2. Keys getting removed.
3. Keys changing their anidation.

The following **could happen**:

1. Keys getting added.
2. Values getting updated.
3. Keys getting deprecated.

### Templates Directory

Skel of structure that sets the values as the key meaning.

#### Extended Attributes

Allows to create fake courses that satisfy complex graph dependencies.

```json
"00": {
    "name": "Ext Attr for Dept 00",
    "comment": "This is a wildcard for strange blocks of courses.",
    "ucampus_code": -1,
    "prefix": {
        "ucampus": [],
        "courses": []
    },
    "xattr": {
        "10": {
            "names": [],
            "depts": [],
            "courses": []
        }
    }
},
```

Given a fake course code `XA0010`:

* `XA` indicates that this fake course only exists on this file and not in U-Campus.

* The first two numbers `00` indicate the department this fake curse belongs to.

* The las two numbers `10` indicate the xattr category of this fake course.

> [!NOTE]
> For more information on xattr check the comprehensive annotations [here](./EXTENDED_ATTR).

#### Major Index Block

Provides information about the available malla versions for the major.

> This allows to iterate through semester files when the filesystem is not exposed e.g. an API for the raw json's.

```json
"v1": {
    "semesters": 14,
    "degrees": {
        "degree1": 6,
        "degree2": 4,
        "degree3": 4
    },
    "malla": "https://faculty.example.com/malla/major/v1",
    "comment": "This is a v1 major malla example."
},
```
#### Degrees

Mallas have available multiples degrees, each of them is represented as a directory holding 1-indexed semesters.

#### Course Block

The minimal unit inside a malla, corresponding to each of the nodes in the major mall graph.

```json
{
    "code": "TC1001",
    "name": "Template Course 1A",
    "credits": 6,
    "concurrent": [],
    "provides": [],
    "requires": [],
    "unlocks": []
},
```

There are two special attributes:

* **concurrent**: The malla requires both blocks to be coursed simultaniously.

* **provides**: A course from an older malla can be convalidated with the present one.

