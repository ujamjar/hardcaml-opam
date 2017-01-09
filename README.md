# v1.2.0

### core

* hardcaml 
* hardcaml-waveterm 
* hardcaml-framework 
* hardcaml-examples 

### simulation

* hardcaml-llvmsim 
* hardcaml-vpi 

### verification

* sattools
* hardcaml-bloop 
* hardcaml-affirm 

### misc

* hardcaml-yosys 
* hardcaml-reedsolomon 

# opam-publish notes

packages needed; publish, ocaml-query

### META file

1. Move pkg/META to pkg/META.in.  
2. Replace `version = "0.1.0"` with `version = "%{version}%"`.
2. Copy META.in to META before local build

### opam file

Add the following fields to opam file

```
name: "hardcaml-waveterm"
version: "0.2.2"
substs:[ "pkg/META" ]
```

And while were at it, add `license: "ISC"`

### makefile 

VERSION      := $$(opam query --version)
NAME_VERSION := $$(opam query --name-version)
ARCHIVE      := $$(opam query --archive)

tag:
	git tag -a "v$(VERSION)" -m "v$(VERSION)."
	git push origin v$(VERSION)

prepare:
	opam publish prepare -r hardcaml $(NAME_VERSION) $(ARCHIVE)

publish:
	opam publish submit -r hardcaml $(NAME_VERSION)
	rm -rf $(NAME_VERSION)

### Release process

Update CHANGES.md and version in opam file.

```
$ make tag prepare publish
```

This will create a pull request on this repository.

### Release to opam

The above could be made to work on the main opam repository, however, for now,
I can just do it manually out of this repo.  

