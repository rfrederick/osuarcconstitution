Instructions
============

I've managed to get the old constitution completely into some fancy new LaTeX code, and it works great. Everything in the document is interlinked (open the PDF and try clicking one of the Table of Contents entries or an in-line article reference). I will briefly outline how this is done in case it isn't clear.

## Contents

Note that the constitution must contain all of the things outlined in the [official example constitution](http://union.okstate.edu/campuslife/Documents/D-SampleConstitutionforStudentOrganizations2012_000.doc) as noted at [http://union.okstate.edu/campuslife/CharteringPacket.htm](http://union.okstate.edu/campuslife/CharteringPacket.htm).

## LaTeX Notes

As a general rule of thumb when editing the LaTeX, just try to follow the format of what I did and nothing should break.

### Article/Section/Subsection Creation

I have defined 3 commands to ease creation of sections and the ability to work with them that should be used throughout the document:
```latex
\myarticle[]{} %for the creation of articles
\mysection[]{} %for the creation of sections
\mysubsection[]{} %for the creation of subsections
```

#### Primary Argument

Each of these commands takes as an argument the relevant name of the section, for instance, `\myarticle{People}` would create the Article People with the appropriate numbering at where it was used. Other than its single optional bracket argument, these commands work just like the `\section{}` command family works.

#### Optional Label

The single *optional* argument of the commands is a label. To use our previous example again, `\myarticle[people]{People}` would create the article People with the label people. Labels allow us to do some fancy document inter-linking, so it's a good idea to use them.

When creating the labels, the convention is:

- Only use lowercase alphanumeric characters
- Try to remain brief
- Every label should be unique

### Document Interlinking and Referencing

(to-do)

### Compilation

The document is set up to be compiled with the latest version of TeX Live 2012 using the included `arara` utility. Simply run the included `arara` binary with `constitution.tex` as the only argument, and the entire document will compile.