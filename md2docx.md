# Overview

This is probably the simplest project. It will just turn one or more markdown
files into a DOCX file using a DOCX template to provide structure, headers
and footers, title page etc.

The version of markdown should support a kind of plugins to allow e.g.
graphviz or plantuml embedded in the input document.

# Features

## Platform-independent

Actually a hard requirement for me is that is has to run on Linux.
I will be using Java, since I know the ecosystem better than C#.

## PEG Parser for Markdown

Building on https://github.com/sirthias/pegdown and MultiMarkdown
(https://github.com/fletcher/MultiMarkdown).

Add extension block syntax to allow inline text-based generation of text or
images (http://www.mattgreer.org/articles/creating-a-pegdown-plugin/).

## Intermediate model

The input will be converted into a document model, which is used for further
steps.

## Model transformation

The model may be transformed with arbitrary plugins, but will still be a
valid document model afterwards.

For now, no model transformations are planned.

## Model output

Finally the model will be transformed into the output format, which is for now
only DOCX.

The heavy lifting for DOCX will be done by https://github.com/plutext/docx4j.

The DOCX output will allow to use a template DOCX input file, so that the
output looks like the template, but with the contents of the input markdown
file.


