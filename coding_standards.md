
# Front End Coding Standards
This document defines formatting and style rules for HTML and CSS. It aims at improving
collaboration, code quality, and enabling supporting infrastructure. It applies to working files that use
HTML and CSS - including pre-processed files such as TWIG, LESS, SASS and SCSS files.

## General Style Rules ##

### Protocol ###
Omit the protocol from embedded resources.

Omit the protocol portion `(http:, https:)` from URLs pointing to images and other media files, style
sheets, and scripts unless the respective files are not available over both protocols.

Omitting the protocol - which makes the URL relative - prevents mixed content issues and results in
minor file size savings.
```
<!-- Not recommended -->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js"></script>

<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

/* Not recommended */
.example {
    background: url(https://www.shopwired.net/images/example);
}

/* Recommended */
.example {
    background: url(//www.shopwired.net/images/example);
}
```

## General Formatting Rules ##

### Indentation ###
Indent by 4 spaces at a time.
Don’t use tabs or mix tabs and spaces for indentation.
```
<ul>
    <li>Fantastic</li>
    <li>Great</li>
</ul>

.example {
    color: blue;
}
```

## Capitalization ##
Use only lowercase.

All code has to be lowercase: This applies to HTML element names, attributes, attribute values
(unless `text/CDATA`), CSS selectors, properties, and property values (with the exception of strings).
```
<!-- Not recommended -->
<A HREF="/">Home</A>

<!-- Recommended -->
<img src="shopwired.png" alt="ShopWired">

/* Not recommended */
color: #E5E5E5;

/* Recommended */
color: #e5e5e5;
```

## Trailing Whitespace ##
Remove trailing white spaces.
Trailing white spaces are unnecessary and can complicate diffs.

```
<!-- Not recommended -->
<p>What? </p>

<!-- Recommended -->
<p>Yes please.</p>
```

## General Meta Rules ##

### Encoding ###
Use UTF-8 (no BOM).

Make sure your editor uses `UTF-8` as character encoding, without a byte order mark.
Specify the encoding in HTML templates and documents via `<meta charset="utf-8">`. Do not specify the encoding of style sheets as these assume `UTF-8`.
(More on encodings and when and how to specify them can be found in Handling characterencodings in HTML and CSS.)

### Comments ###

Explain code as needed, where possible.

Use comments to explain code: What does it cover, what purpose does it serve, why is respective solution used or preferred?

(This item is optional as it is not deemed a realistic expectation to always demand fully documented code. Mileage may vary heavily for HTML and CSS code and depends on the project’s complexity.)

### Action Items ###
Mark todos and action items with `TODO`.

Highlight todos by using the keyword `TODO` only, not other common formats like `@@`.

Append a contact (username or mailing list) in parentheses as with the format `TODO(contact)`.

Append action items after a colon as in `TODO: action item`.

```
<!-- TODO: Add Category names -->
<ul>
    <li>Lorem</li>
    <li>Ipsum</li>
</ul>
```

## HTML Style Rules ##

---

We use Foundation v6.3 with the ['Float Grid'](https://foundation.zurb.com/sites/docs/grid.html).

Becuase support for Internet Explorer 9+ is required, please avoid using the ’Flex’ or ‘XY’ grids.
