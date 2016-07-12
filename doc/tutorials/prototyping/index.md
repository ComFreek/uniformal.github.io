---
layout: doc
title: Defining a Formal System in MMT
---

In this tutorial, we build an implementation of first-order logic (FOL) in MMT.

It assumes that

* MMT has been [installed](../../setup),
* archives are placed in some folder, which is refered to as `CONTENT`,
* [jEdit](../../applications/jedit) is used for editing mmt files.<span class="detail">Other editors will work but might make editing awkward.</span>

### Define a Meta-Logic

Actually, we will skip this step because only advanced need to define their own meta-logic.

Instead, we can choose one of the meta-logics already defined in MMT.
The most important example is the logical framework LF, whose MMT URI is
`http://cds.omdoc.org/urtheories?LF`.

This theory is defined in the archive MMT/urtheories, which is automatically cloned into the folder CONTENT when setting up MMT.

<div class="detail" markdown="1">
Other important meta-logics defined in this archive include

* `http://cds.omdoc.org/urtheories?PLFextends` LF with shallow polymorphism
* `http://cds.omdoc.org/urtheories?LFModulo`, which extends LF with a rewrite system

These can also be combined.
</div>

For FOL, LF is sufficient as a meta-logic.

### Define the Formal System in an Appropriate Meta-Logic

We create a new file `fol.mmt`, in which we will define FOL.

#### Creating the File

It does not matter where this file is located.
But to allow for running MMT build targets over it later, it is convenient to place it in a new MMT archive:

* create a folder `CONTENT/MYARCHIVE`
* create a file `MANIFEST.MF` in it containing (at least) the line `id: MYARCHIVE`,
* and create a file `source/fol.mmt` in it

#### Create a Theory for FOL

Open the file in jEdit and create an empty theory:

```
namespace http://mydomain.org/mmt-example [GS]

theory FOL : http://cds.omdoc.org/urtheories?LF =

[GS]
```

Here

* The `namespace` declaration defines a unique namespace (a URI) for our example.<span class="detail">The URI does not have to be a URL, i.e., it does not have to point to a physical location. It only acts as a unique identifier.</span> 
* The `theory` introduces an MMT theory called `FOL` with meta-theory `http://cds.omdoc.org/urtheories?LF`.<span class="detail">Alternatively, we can write `ur:?LF` because the namespace prefix definition `import ur http://cds.omdoc.org/urtheories [GS]` is implicitly present.</span>
* `[GS]` refers to ASCII 29, the toplevel [delimiter](../../language/delimiters.html) used by MMT.
  In jEdit, it can be inserted via the symbol button for it or by typing `jGS `.


#### Define the Syntax and Semantics of FOL

From this point on forwards, defining a language proceeds according to LF.

The details of doing so are not part of this tutorial.
However, the file `tutorial.mmt` in the archive `CONTENT/MMT/examples` is a self-documented example of how to do it.
This archive is automatically cloned when setting up MMT.

It is good practice to copy over this example step by step.

#### View the Logic in the Browser

We can start the MMT web server from within jEdit to view our definition in the browser:

* go to the jEdit plugin called console
* choose mmt as the console language
* type `server on 8080` (or some other port number)
* point the browser to [http://localhost:8080?]

#### Build and Serve the Archive


### Implement a FOL Plugin

MMT can provide many important algorithms generically.
But occasionally, we want to provide language-specific functionality explicitly.

MMT goes out of its way to open up as many internal details to plugin interfaces as possible.


