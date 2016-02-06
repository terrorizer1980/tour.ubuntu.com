# How to create translated HTML pages

You simply need to go to the translate-html/bin folder and run:

./translate-html -t

This will generate a set of folders, one for each available translations,
ready to publish online

# Translate script help

translate-html/bin$ ./translate-html --help
Usage: translate-html {--extract|--translate} [options]

    This script can be used to prepare translatable messages in HTML files
    and expose them to translators and to subsequently use those translations
    to build localized HTML files based on the original in English.

    It works in one of two modes:

    - Extract mode: extracts translatable strings from the file specified
      in the 'po/POTFILES.in' file and puts them into a .pot file into the
      'po' folder, ready to give it to translators.
    - Translate mode: fetches the translations in the form of .po files in the
      'po-html' folder and builds localized files based on the original.
      Untranslated strings in the PO files are left as their English originals
      in the generated localized files. The localized files are named
        <ISO-639-2-lang-code>/<original-filename>.<original-fileext>
      E.g.
        en/index.html      <- original file
        zh-CN/index.html   <- Simplified Chinese translation

    Structure of the 'po-html' folder:

      po-html/template.pot <- translation template created in extract mode
      po-html/POTFILES.in  <- files to extract strings from are specified here
      po-html/zh_CN.po     <- translation done by translators
      po-html/ca.po        <- another translation, naming: <ISO 639-2 code>.po



Options:
  --version        show program's version number and exit
  -h, --help       show this help message and exit
  -d, --debug      Print the maximum debugging info (implies -vv)
  -v, --verbose    set error_level output to warning, info, and then debug
  -x, --extract    Extract mode: extract the strings from the original HTML
                   file
  -t, --translate  Translate mode: get the translations from PO files and
                   write them to a new translated HTML file
  -s, --test       Test mode: only effective in conjunction with Translate
                   mode. If set, untranslatable messages are translated as
                   reversed English, so that they are easy to spot.

# Running the site

The site is just flat HTML pages, so running the site is as easy as
opening `en/index.html` with a browser, or running a simple server, e.g.:

``` bash
python -m SimpleHTTPServer 8000
```

And visiting <http://localhost:8000>.

# Compressing the site

To ensure the Online Tour is optimised for page weight download and onload performance,
there are some Gulp tasks available:

* `compress-html`: Minify CSS and JS, and bundle it in with the HTML
* `compress-images`: Optimise image files to make them smaller
* `compress-all`: Run both of the above actions

*NB:* `compress-html` will modify HTML files in-place, so you may lose any changes.

To get started, install all the required node modules;

```
npm install
```

Then run Gulp to perform the tasks specified above;

```
gulp {action}
```

