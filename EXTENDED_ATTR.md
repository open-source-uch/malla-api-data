# Extended Attributes

Compatibility layer with U-Campus that simplifies complex graph dependencies.

The code `XAddgg` is separated in three components:

* `XA`:
    * Extended Attributes Course.
    * Mapped to the xattr file.

* `dd`:
    * Department code for the course.
    * Each char follows the regex `[0-9]`.

* `gg`:
    * Group of courses that satisfy it.
    * Each char follows the regex `[0-9A-Z]`.

> [!IMPORTANT]
> Unlike the `provides` attribute in a code block, the `gg` component groups active U-Campus courses that satisfy the same node inside a malla graph.