# pdf-fx-epub3

This Bash shell script uses the *pdf-fx-epub3* (based on #pdf2epubEX) tool to convert a PDF file to an ePub file.

The result is a *fixed layout* ePub version 3: the layout is perfectly retained and all the fonts are embedded.

The *pdf-fx-epub3* tool converts a PDF file into HTML5 (with CSS, JS, fonts, and bitmap and/or vector images).

Once you have an ePub file, only if you want, you can edit it with one of the available tools (Sigil, Calibre, Kotobee, etc.) to add interactive content, add reflowable text, etc.

If you want to publish an eBook on one of the available eBook stores (Google Play Books, Apple Books, Rakuten Kobo, etc.), you have to provide an ePub file and not a PDF file.

### Installation

You need to install Docker which is available for all computer operating systems: Linux, Windows and MacOS. See [here](https://docs.docker.com/engine/install).

Remark: You will first have to install WSL1 (Windows Subsystem Linux), then update to WSL2.

## For Windows

### Usage

To convert C:\Users\UserName\Documents\myfile.pdf to C:\Users\UserName\Documents\myfile.epub, open a terminal in the root folder (PowerShell, Command Prompt or Windows terminal) and run the following commands:

```
docker build . -t imeysam-sh/pdf-fx-epub3
docker run -ti --rm -v C:\Users\UserName\Documents:/temp imeysam-sh/pdf-fx-epub3 pdf2epubEX myfile.pdf
```

## Parameters

Once you launch *pdf2epubEX*, some information will be displayed like the book/PDF width and height (in inches and cm), then some questions will be asked like:

- Format of the images in the epub (png, jpg or svg) [default: jpg]
- Resolution of the images in the epub in dpi (e.g.: 150 or 300) [default: 150]
- Title, author, publisher, year, language, ISBN number, subject

If you want, you can hit `ENTER` to all the questions.

Image formats:

- if you chose png or jpg (bitmap formats), the vector images of the PDF will be converted in bitmap images (rasterized).
- if you chose svg (vector and bitmap format), the vector images of the PDF will remain in vector format, but: a) you cannot chose the resolution of the bitmap images (it is the one from the PDF); b) the bitmap images will be included in the svg files (Base64 coded); c) this format is not always correctly rendered by eBook readers; d) the generated epub file is not always passing the epub check.

A vector image can be as simple as a line, a rectangle, a table frame, a colored background, etc.

For eBooks with a lot of bitmap images, it is better to chose JPG (compression with loss) to not have a file too big. For eBooks with mainly vector images, it is better to chose PNG (lossless compression).
