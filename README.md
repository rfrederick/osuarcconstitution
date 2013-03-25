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
\myarticle[]{}    % for the creation of articles
\mysection[]{}    % for the creation of sections
\mysubsection[]{} % for the creation of subsections
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

Any time you want to refer to another article in the constitution, you should always do so by referencing the relevant article's label. In addition to being the LaTeX equivalent of good coding practice, this also allows some useful features. For instance, since the entire document is written by this method, if I wanted to add a new Article I (and therefore push all the other articles up a number), I could simply add the article at the beginning with the `\myarticle{}` command. Then, since we used this label and referencing system, if I had referenced Article II in one part of a document, it would automatically change it to say Article III to meet the new numbering. The other thing this allows us to do is interlink the document. This means that simply clicking a reference to "Article IV" would actually take us to Article IV in the document.

#### Commands

This is all done using 3 basic commands (these can be used for articles, sections, and subsections):
```latex
\hyperref[]{} % This allows us to link to an article
              % and control the text that is linked to

\autoref{}    % This creates the text that refers to an
              % article based on its label, and will 
              % optionally link to the article as well

\ref{}        % This does the same as \autoref, but only
              % creates the alphanumerical representation
              % (eg. referencing the label for Article III
              % would output III here)
```
#### Labels

Before I elaborate on the commands, it is necessary to explain how to find the labels I will be referring to: all the base-labels can be found as the argument in brackets of the corresponding article, section, or subsection creation command (as referred to above). However, there is an additional label prefix that you need to add when actually referencing these labels; using `label` as a placeholder text, this is as follows when referencing an article, section, or subsection respectively:

```
art:label
sec:label
sub:label
```

#### \autoref{}

`\autoref{}` is the primary command used to refer to the basic text of an article. Its only curly-braced argument is the full prefixed label of the item you want to state the name of. For example, if Article IV is declared by `\myarticle[bylaws]{By-Laws}`, and we wanted to refer to Article IV in the document and link to it, we would do this with the code `\autoref{art:bylaws}`. This would simply display the text `Article IV` in the compiled document where you placed this code. Additionally, it will make it so clicking that text will "link" you to Article IV. Linking a section and subsection works similarly. If Section B in the compiled document is defined with `\mysection[minlaw]{Minimum Contents of the By-Laws}`, then `\autoref{sec:minlaw}` will display the text `Section B`. One useful feature of this command is the so-called "star" variant. By adding a "star" (*) to the end command, we can make the compiled document display the text *without* it linking to anything. Using the previous example, `\autoref*{sec:minlaw}` would display the text `Section B` without a link. By using `\autoref{}`, we ensure we will always be referring to the correct section, even if document ordering changes.

#### \hyperref[]{}

`\hyperref[]{}` works similarly to `\autoref{}`, but serves a different purpose. The `\hyperref[]{}` command does *not* display any text, but is only used to create links to a specific part of the document. This can be used to link any text in the document to any other part of the document. It does this through two arguments. First, it has a bracketed argument that will contain full prefixed label of the item you want to link to, and second, it has a curly-braced argument that contains the text of the link. So, using our previous example, if we wanted to make the text `click here` link to Article IV on By-Laws (declared by `\myarticle[bylaws]{By-Laws}`), we would use the code `\hyperref[art:bylaws]{click here}`. This will only display the text `click here` in the compiled document, but clicking the text will jump you to the article on bylaws. In practicality, this command is useful to link a string of text to a specific article. For example, if we were trying to tell somebody reading the constitution to look at a specific section in the By-Laws article, for instance `Article IV, Section B` (Article IV defined as above, Section B defined with `\mysection[minlaw]{Minimum Contents of the By-Laws}`), we could adequately display this text using two `\autoref{}` commands, but this would present an unexpected user experience: a user clicking the first part of that text might expect to be jumped to Section B, but would instead be taken to Article IV. Additionally, the comma and spacing isn't a link at all. Ideally, the entire phrase would be a link to Section B. Luckily, by combining our "starred" variants of `\autoref{}` with `\hyperref[]{}`, we can do this. Here's the code: `\hyperref[sec:minlaw]{\autoref*{art:bylaws}, \autoref*{sec:minlaw}}`. This displays the text `Article IV, Section B`, and the entire thing will link to Section B.

#### \ref{}

You will probably *not* need to use this, but it can be useful if you want to refer to an article in a sort of shorthand. In short, this works *exactly* like `\autoref{}`, but it will display the alphanumerical representation without the prefix of Article/Section/etc. As an example, if Article IV had the label bylaws, then `\ref{art:bylaws}` would display the text `IV`, and the text would link to Article IV.

### Compilation

The document is set up to be compiled with the latest version of TeX Live 2012 using the included `arara` utility. Simply run the included `arara` binary with `constitution.tex` as the only argument, and the entire document will compile. Alternatively, the document can simply be compiled with several passes of `pdflatex`.