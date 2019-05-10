# tex_signature
A small Tex-package to generate digital Signatures

## Dokumentation

Until I find time to write a proper README, checkout my [Blog-Post](http://akuederle.com/create-professional-signature-with-latex/) about this project!

## Installation

The installation process is basically identical to other custom Latex packages. Depending on the Latex distribution you are using, there might be some variance.

First, find your local *texfm* tree. You can usually do that by typing ```kpsewhich -var-value=TEXMFHOME``` into your console.
If the listed directory does not exist, create it. Inside the folder create a subfolder called *tex* and inside this one another folder called *latex*.

```
localtexfmtree/texfm/tex/latex/
```

Now you can put (or symlink) all your custom Latex packages into this folder (or any subdirectory of it). If you are using *texlive*, that is all you have to do. In case of *Miktex* you have to refresh the local package database. Please check the documentation for your operation system, on how to do this.

In the special case of this package, I would suggest to move or clone the whole gitrepo into your texfm tree. The only thing left now, is to create your own signatures.

## Usage

### Making your own signature

By default all the signatures have to be stored in the *signatures* subdirectory relative to the *mysignatures.sty* file. You can change this by manipulation the following line of the mysignature.sty file.
```latex
\input{signatures/\mysignature@signature} % loads the respective settings file
```

A signature consists of an settings .tex file and a PNG of your written signature. The name of the settings file is used to refer back to the signature.
The settings file must contain the following lines:

```Latex
\def\SigName{Hans Mueller} % The Name
\def\SigLocation{Frankfurt am Main} % The city
\def\SigJob{Boss of Everything} % The Job/ position
\def\SigSource{signatures/test_signature.png} % Path to the scanned signature
\def\SigTransformX{0px} % Length the signature is moved in X direction from the default location
\def\SigTransformY{-5px} % Length the signature is moved in Y direction from the default location
```

The values of the different parameters can of course be changed! Regarding the the path to the picture, keep in mind how relative paths inside packages are handeld in Latex.

```Latex
.\folder\file % this is interpreted relative to Main file (probably not what you want in this case!)
folder\file % this is interpreted relative to the package file the input or include command is used in.
```

To get the path to your picture right, specify it relative to the .sty file. So if you put the picture in the same folder as the settings-file, use: *signatures/pciturename.png*

### Include the signature

To use the package, you have to import it as every other package.
Optional import options are:
- signature="Name of siganture to use" - default is "default_siganture"
- date="Date to display above the signature" - if not specified \today is used. If specified without value the date of the maindocument is used
- nolocation - switch, hides the location
- nojob - switch, hides the job
- empty - switch, hides the written signature

An example import looks like this:

```latex
\usepackage[signature=mytestsignature, date=12.3.2014, nojob]{mysignature}
```

To create the signature use the ```\mysignature``` command inside your document. It takes one optional argument to specify the position and one mandatory argument to specify the style. Possible values for the position are: left, right, center. Available styles are *minimal* or *full*.

```latex
\mysignature[left]{full}
```
