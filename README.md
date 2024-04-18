# texifypdfs
Bash script to process pdfs which include math text, via Inkscape, for inclusion in LaTeX documents.

## Use case for texifypdfs
Suppose you are making an image (or images) for a math article, on your iPad, using eg Notability. You want to include this image
into your LaTeX paper, `article.tex`, in such a way that text in the image will be texified by LaTeX, using the Inkscape text -> LaTeX feature. 
In other words, a text box $\int_a^b x^2 dx$ in your Notability drawing will be included in your article as a picture where LaTeX has processed
the math. 

You want to do this all automatically, in such a way that every time you edit the image in Notability, changes will be pushed into your `article.tex` file.

## Workflow

So, what you do is you switch on cloud storage, say Box (or Dropbox, or...), in Notability, so that your Inkscape drawing (a .note file) gets exported automatically as a pdf into
a folder on Box in the cloud, say `Notability/images/image1.pdf`.

Then you install the desktop application for Box on your pc, so that image1.pdf now gets automatically downloaded onto your desktop. On a Mac, using Box, this would be located 
in the folder `/Users/username/Library/CloudStorage/Box/Notability/images`. (Replace username with your user name).

Ok. Now, in the folder where your `article.tex` file is located, you run the following command from a terminal:

```
texifypdfs /Users/username/Library/CloudStorage/Box/Notability/images
```

The script then goes to that folder, and processes the pdfs (using Inkscape) into pairs (pdf file with text removed, latex file for inclusion).  So the file `image1.pdf` in the `/Users/username/Library/CloudStorage/Box/Notability/images` folder will get processed into the pair of files `image1.pdf` (which won't have text in it) and `image1.pdf_tex` (which will have the text in it in LaTeX form), which you include into `article.tex` via the `\input{image1.pdf_tex}`. There we go!

Each time you run the script, it only processes the pdf files which have been updated since the last time the script was run. So no unnecessary Inkscape calls are made.

To be extra convenient, you can put incorporate a call to texifypdfs as part of your build script for your LaTeX file. 

## notewatch

The script `notewatch` is a bit different. It actively monitors the cloud folder on your desktop (in our case above, `/Users/username/Library/CloudStorage/Box/Notability/images`) and when pdfs are added or updated there, it runs Inkscape on them to latexify them. 

## Requirements

You need to have Inkscape installed and in your path.



 
