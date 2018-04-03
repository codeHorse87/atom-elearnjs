# Atom elearn.js

This package converts Markdown files to HTML and PDF and is specifically
designed to use [elearn.js](https://github.com/elb-min-uhh/elearn.js) for styling
and interactive elements.

## Installation

Simply search for `atom-elearnjs` in Atom's Settings view to install this
package.

## Usage

In Atom open your Markdown file. Afterwards you can do any of the following:

* use the Package tab, access elearn.js and convert to either html or pdf.
* Right-Click in the editor window and choose `elearn.js - to HTML` or
`elearn.js - to PDF`
* Convert with hotkeys:
    * To HTML: `ctrl-alt-o`
    * To PDF: `ctrl-alt-p`

## Additions to Markdown Syntax

To use additional elearn.js features or add meta information or
scripts to the HTML Head you can use the following syntax.

### Sections

Sections are automatically created at headings. These sections are used by
_elearn.js_ to create pages. This can be changed in the
_settings_ of this atom package. By default headings up to `### Heading 3`
will start a new section with the name set to the headings text.

If you only want a specific heading to not start a new section, insert
`<!--no-section-->` into the headings text like this:

    ## Example Heading <!--no-section-->

If you disable this option or want a new section at a specific point, you can
insert

    |||SECTION_NAME///

This way the html will contain a surrounding `<section name="SECTION_NAME">`.

__Notice:__ You should always insert the first section before everything else
(besides not displayed elements like the _meta information_ or _imprint_ below).
Other displayed elements before the first section will otherwise always be
visible.

### Meta Information

The following block has to be added to the markdown file (preferably at the top)
to add meta information to the generated HTML-File.

    ---
    Title: elearn.js Template
    Author: Name Author
    Description: Enter Descriptions
    Keywords: Key, Words
    Custom: "<script type=\"text/x-mathjax-config\">
                MathJax.Hub.Config({
                    extensions: [\"tex2jax.js\"],
                    jax: [\"input/TeX\", \"output/HTML-CSS\"],
                    tex2jax: {
                        inlineMath: [ ['$','$'], [\"\\(\",\"\\)\"] ],
                        displayMath: [ ['$$','$$'], [\"\\[\",\"\\]\"] ],
                        processEscapes: true
                    },
                    \"HTML-CSS\": { availableFonts: [\"TeX\"] }
                });
            </script>
            <script type=\"text/javascript\"
                src=\"https://cdn.mathjax.org/mathjax/latest/MathJax.js\"></script>"
    ---

This will basically add `<meta>` elements to the HTML's Head.
For example `Author: Name Author`, where `Author` might be called _Key_ and
`Name Author` _Value_, will be converted to
`<meta name="author" content="Name Autor"/>`. There are only two exceptions to
this rule.

* `Title` will convert to a `<title>` element.
* `Custom` will add the value without any conversion to the Head.
In this example the MathJax Script is loaded and initiated.

If you want to write a value over multiple lines you can surround it with `'`
or `"` otherwise it will only get interpreted as single line value. The chosen
wrapper has to be escaped within the value. This can also be seen in the example
above. Another example: `Title: An "Example" with quotes` is equal to
`Title: "An \"Example\" with quotes"` and `Title: 'An "Example" with quotes'`.

The `---` wrapping the block is necessary if you include this block.
All Key-Value pairs have to be within these `---` lines. If you want to be sure
the block will not be converted to anything else by other converters you can
also use the alternative syntax:

    <!--meta
      Title: elearn.js Template
      Author: ...
    -->

This way you are save to use this even when working with other converters. But
you cannot use `-->` in the block and atom will not highlight the syntax.

All fields are optional as well as the block itself.


### elearn.js Imprint

In the HTML version's menu of an elearn.js document is an imprint. To add your
imprint information you have to add the following block to the markdown code.

    <!--imprint
      YOUR CODE HERE
    -->

Within this block either markdown or html is allowed.

This block is optional but it is recommended to insert this block at the top of
your markdown file. This block should not be converted in other markdown
converters due to its html comment style. This way you are save to use
this even when working with other converters. But of course other converters
will not generate any output based on this block.
There are two alternatives to this syntax:

    ```imprint
      YOUR CODE HERE
    ```

and

    ~~~imprint
      YOUR CODE HERE
    ~~~

## Planned Features

* Add settings for:
    * _HTML and PDF_:
        * Filechooser for output location
        * Optional MathJax integration
        * Optional CSS File for additional styles
    * _HTML only_:
        * Optional export of _elearn.js_ assets
        * Optional export of linked files into _elearn.js_ assets
    * _PDF only_:
        * Optional footer text

## Known Issues

* All platforms:
    * PDF output might break elements at page end (e.g. lines might be broken
        horizontally)
        * Workaround: add forced page break `<div style="page-break-before: always;"></div>`
* Linux/Mac OS:
    * PDF output is zoomed
        * Workaround: zoom factor ~0.7
    * PDF output has no footer/page numbers.

## Credits

* [Atom](https://atom.io) the editor you need!
* [Showdown](http://showdownjs.com/) used for Markdown to HTML conversion.
* [marcbachmann/node-html-pdf](https://github.com/marcbachmann/node-html-pdf)
used for HTML to PDF conversion.

## License

atom-elearnjs is developed by
[dl.min](https://www.min.uni-hamburg.de/studium/digitalisierung-lehre/ueber-uns.html)
of Universität Hamburg.

The software is using [MIT-License](http://opensource.org/licenses/mit-license.php).

cc-by Michael Heinecke, Arne Westphal, dl.min, Universität Hamburg
