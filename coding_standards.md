
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

### Document Type ###
Use HTML5.
HTML5 (HTML syntax) is preferred for all HTML documents: `<!DOCTYPE html>`.
(It’s recommended to use HTML, as `text/html`. Do not use XHTML. XHTML, as `application/xhtml+xml`, lacks both browser and infrastructure support and offers less room for optimization than HTML.)

Although fine with HTML, do not close void elements, i.e. write `<br>`, not `<br />`.

### HTML Validity ###
Use valid HTML where possible.
Use valid HTML code unless that is not possible due to otherwise unattainable performance goals regarding file size.
Use tools such as the W3C HTML validator to test.
Using valid HTML is a measurable baseline quality attribute that contributes to learning about technical requirements and constraints, and that ensures proper HTML usage.
```
<!-- Not recommended -->
<title>Test</title>
<article>This is only a test.

<!-- Recommended -->
<!DOCTYPE html>
<meta charset="utf-8">
<title>Test</title>
<article>This is only a test.</article>
```

### Semantics ###
Use HTML according to its purpose.

Use elements (sometimes incorrectly called “tags”) for what they have been created for. For example, use heading elements for headings, p elements for paragraphs, a elements for anchors, etc.
Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.
```
<!-- Not recommended -->
<img src="spreadsheet.png">

<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

### Multimedia Fallback ###

Provide alternative contents for multimedia.

For multimedia, such as images, videos, animated objects via `canvas`, make sure to offer alternative access. For images, that means use of meaningful alternative text (`alt`) and for video and audio transcripts and captions, if available.

Providing alternative contents is important for accessibility reasons: A blind user has few cues to tell
what an image is about without `@alt`, and other users may have no way of understanding what video
or audio contents are about either.

(For images whose `alt` attributes would introduce redundancy, and for images whose purpose is
purely decorative which you cannot immediately use CSS for, use no alternative text, as in `alt=""`.)

### Separation of Concerns ###

Separate structure from presentation from behaviour.

Strictly keep structure (markup), presentation (styling), and behaviour (scripting) apart, and try to keep
the interaction between the three to an absolute minimum.

That is, make sure documents and templates contain only HTML and HTML that is solely serving
structural purposes. Move everything presentational into style sheets, and everything behavioural into
scripts.

In addition, keep the contact area as small as possible by linking as few style sheets and scripts as
possible from documents and templates.

Separating structure from presentation from behaviour is important for maintenance reasons. It is
always more expensive to change HTML documents and templates than it is to update style sheets
and scripts.
```
<!-- Not recommended -->
<!DOCTYPE html>
<title>HTML sucks</title>
<link rel="stylesheet" href="base.css" media="screen">
<link rel="stylesheet" href="grid.css" media="screen">
<link rel="stylesheet" href="print.css" media="print">
<h1 style="font-size: 1em;">HTML sucks</h1>
<p>I’ve read about this on a few sites but now I’m sure:</p>
<u>HTML is stupid!!1</u>
<center>I can’t believe there’s no way to control the styling of my website without
doing everything all over again!</center>

<!-- Recommended -->
<!DOCTYPE html>
<title>My first CSS-only redesign</title>
<link rel="stylesheet" href="default.css">
<h1>My first CSS-only redesign</h1>
<p>I’ve read about this on a few sites but today I’m actually doing it: separating
concerns and avoiding anything in the HTML of my website that is presentational.</p>
<p>It’s awesome!</p>
```

### Entity References ###
Do not use entity references.

There is no need to use entity references like `&mdash;`, `&rdquo;`, or `&#x263a;`, assuming the same
encoding (UTF-8) is used for files and editors as well as among teams.

The only exceptions apply to characters with special meaning in HTML (like `<` and `&`) as well as
control or 'invisible' characters (like no-break spaces).
```
<!-- Not recommended -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.

<!-- Recommended -->
The currency symbol for the Euro is '€'.
```

### Optional Tags ###
While current standards designate certain closing elements and even document level elements as
optional, use all open and closing elements nested in the correct ways to ensure maximum
compatibility and clarity of document structure.

Generally speaking, self-closing XML (i.e. XHTML, XML) style tags are not necessary.

```
<!-- Not recommended - closing "/" is not necessary -->
<img src="/logo.png" alt="Shopwired">

<!-- include closing tags, however -->
<p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit:
</p>
<ul>
    <li>Vero sunt veritatis magni sit odit,</li>
    <li>voluptatum ratione suscipit.</li>
</ul>
```

### Type Attributes ###
Omit `type` attributes for style sheets and scripts.

Do not use `type` attributes for style sheets (unless not using CSS) and scripts (unless not using
JavaScript).

Specifying `type` attributes in these contexts is not necessary as HTML5 implies `text/css` and
`text/javascript` as defaults. This can be safely done even for older browsers.

```
<!-- Not recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css” type="text/css">

<!-- Recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css">

<!-- Not recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>

<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
```

## HTML Formatting Rules ##
