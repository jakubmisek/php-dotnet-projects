**Dompdf is an HTML to PDF converter**

At its heart, dompdf is (mostly) a [CSS 2.1](http://www.w3.org/TR/CSS2/) compliant
HTML layout and rendering engine written in PHP. It is a style-driven renderer:
it will download and read external stylesheets, inline style tags, and the style
attributes of individual HTML elements. It also supports most presentational
HTML attributes.

----

**Check out the [demo](https://dompdf.net/examples.php) and ask any
question on [StackOverflow](http://stackoverflow.com/questions/tagged/dompdf) or
on the [Google Groups](http://groups.google.com/group/dompdf).**

Follow us on [![Twitter](http://twitter-badges.s3.amazonaws.com/twitter-a.png)](http://www.twitter.com/dompdf).

---

## Features

 * Handles most CSS 2.1 and a few CSS3 properties, including @import, @media &
   @page rules
 * Supports most presentational HTML 4.0 attributes
 * Supports external stylesheets, either local or through http/ftp (via
   fopen-wrappers)
 * Supports complex tables, including row & column spans, separate & collapsed
   border models, individual cell styling
 * Image support (gif, png (8, 24 and 32 bit with alpha channel), bmp & jpeg)
 * No dependencies on external PDF libraries, thanks to the R&OS PDF class
 * Inline PHP support
 * Basic SVG support (see "Limitations" below)
 
## About Fonts & Character Encoding

PDF documents internally support the following fonts: Helvetica, Times-Roman,
Courier, Zapf-Dingbats, & Symbol. These fonts only support Windows ANSI
encoding. In order for a PDF to display characters that are not available in
Windows ANSI, you must supply an external font. Dompdf will embed any referenced
font in the PDF so long as it has been pre-loaded or is accessible to dompdf and
reference in CSS @font-face rules. See the
[font overview](https://github.com/dompdf/dompdf/wiki/About-Fonts-and-Character-Encoding)
for more information on how to use fonts.

The [DejaVu TrueType fonts](https://dejavu-fonts.github.io/) have been pre-installed
to give dompdf decent Unicode character coverage by default. To use the DejaVu
fonts reference the font in your stylesheet, e.g. `body { font-family: DejaVu
Sans; }` (for DejaVu Sans). The following DejaVu 2.34 fonts are available:
DejaVu Sans, DejaVu Serif, and DejaVu Sans Mono.

## Quick Start

Just pass your HTML in to dompdf and stream the output:

```C#
// instantiate and use the dompdf class
var dompdf = new Dompdf.Dompdf();

dompdf.loadHtml("<h1>hello world</h1>");

// (Optional) Setup the paper size and orientation
dompdf.setPaper("A4", "landscape");

// Render the HTML as PDF
dompdf.render();

// Get the generated PDF into a byte array
var pdf = dompdf.output(default).ToBytesOrNull();
```

### Setting Options

Set options during dompdf instantiation:

```c#
var options = new Dompdf.Options();
options.set("defaultFont", "Courier");
dompdf = new Dompdf.Dompdf(PhpValue.FromClass(options));
```

or at run time

```c#
var dompdf = new Dompdf.Dompdf();
var options = dompdf.getOptions().Cast<Dompdf.Options>();
options.setDefaultFont("Courier");
dompdf.setOptions(options);
```

See [Dompdf\Options](https://github.com/dompdf/dompdf/blob/master/src/Options.php) for a list of available options.


## Limitations (Known Issues)

 * Dompdf is not particularly tolerant to poorly-formed HTML input. To avoid
   any unexpected rendering issues you should either enable the built-in HTML5
   parser at runtime (`options.setIsHtml5ParserEnabled(true);`) 
   or run your HTML through a HTML validator/cleaner (such as
   [Tidy](http://tidy.sourceforge.net) or the
   [W3C Markup Validation Service](http://validator.w3.org)).
 * Table cells are not pageable, meaning a table row must fit on a single page.
 * Elements are rendered on the active page when they are parsed.
 * Embedding "raw" SVG's (`<svg><path...></svg>`) isn't working yet, you need to
   either link to an external SVG file, or use a DataURI like this:
     ```php
     html = '<img src="data:image/svg+xml;base64,' . base64_encode($svg) . '" ...>';
     ```
     Watch https://github.com/dompdf/dompdf/issues/320 for progress

---

[![Donate button](https://www.paypal.com/en_US/i/btn/btn_donate_SM.gif)](http://goo.gl/DSvWf)

*If you find this project useful, please consider making a donation. Any funds donated will be used to help further development on this project.)*
