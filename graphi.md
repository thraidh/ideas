# Overview

This idea is about a system, that generates graphs, pictures, diagrams and
other things you'd usually draw with something like Visio or Powerpoint.
It does this by processing one or more text files which describe what should
be in the resulting picture.
In contrast to ususal systems converting a textual description into a picture
this system is more sophisticated, in that it will aid the user in placement
of the picture element, so you describe only what is in the picture, but not
exactly how it looks. This is comparable to what (La)TeX does, where you also
just describe what you want, and (La)TeX takes care of how it looks.

This system is especially useful for generating pictures from data which is
already present somewhere. Therefore there is always an input model which is
transformed into a picture model which is transformed into the resulting
picture.

This system will therefore also provide access to several inputs like text
files, databases, HTTP APIs, binary files and maybe more. In addition there
are ways to unify these inputs and convert the input model into a suitable
model.


