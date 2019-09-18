---
title: okralact - a multi-engine Open Source OCR training system
tags: OCR-D
description: Yeah.
slideOptions:
  theme: blood
  spotlight:
    enabled: false
---

<style>
.kb-hi { 
	color: red;
	background-color: #00000088;
}
.dark-bg {
	background-color: #00000088 !important;
}
.light-bg {
	background-color: #ffffff88 !important;
}
</style>

# okralact

### a multi-engine Open Source OCR training system

<img src="http://ocr-d.de/sites/default/files/Header1-Text-gold_4.png"/>

Slides: https://hackmd.io/@6BN9tdLhQSWPUeUaTvNkaw/SyiQKUCUH

---

<!-- .slide: data-background="https://raw.githubusercontent.com/kba/2019-icdar/master/ajw6qfdhxt5e4ltqqm4c.jpg?token=AACCXVYDRIMEQMRIPFGF6525RLUU2" -->

<div style="font-family: monospace; white-space: pre; font-size: 2.4em">
       <strong class="kb-hi">O</strong>cropus            
       <strong class="kb-hi">kra</strong>ken             
     ca<strong class="kb-hi">la</strong>mari             
tessera<strong class="kb-hi">ct</strong>              
</div>

----

### OCRopus

![](https://github.com/kba/2019-icdar/raw/master/687474703a2f2f6d61646d2e64666b692e64652f5f6d656469612f6f63726f7075732e706e67)

* @tmbdev since 2007 (ocropy: 2010)
* Standout features:
	* often used, lots of documentation and wrappers (e.g. Ocrocis)
	* CLI tools: `ocropus-nlbin`, `ocropus-gtedit` etc.

----

### kraken

![](https://raw.githubusercontent.com/kba/2019-icdar/master/1*3Trbay07WLA99_czXxn_yA.jpeg?token=AACCXVYDRIMEQMRIPFGF6525RLUU2)

* @mittagessen since 2015
* Standout features:
	* Clean codebase, documentation and interfaces
	* CLI tools: `kraken binarize`, `ketos transcribe` etc.

----

### calamari 
<p>
	<img class="light-bg" src="https://avatars1.githubusercontent.com/u/40763252?v=4" height="200"/>
</p>

* by @CHWick
* Created: 2018

----

### tesseract

<p>
	<img src="https://user-images.githubusercontent.com/33478216/39959054-aa7b6138-5614-11e8-9961-25d137dcb43b.jpg" height="200"/>
</p>

* by @theraysmith
* Created: 1985 (LSTM: 2016)


---

<!-- .slide: data-background="https://petapixel.com/assets/uploads/2015/04/octopus.jpg" -->
<!-- .slide: class="dark-bg" -->

# Training

----

## Basic Approach

* Produce line-based Ground Truth (GT)
* Feed into training engine:
  * line text and image from GT
  * neural network structure
  * language model

----

## Different Conventions (examples)

* File name and folder structure schemes
* Neural network setup
* Training stop conditions

----

## Case in Point: tesstrain

* Started in 2018 as Makefile to make tesseract 4.0 training manageable
* Grown to include lots of optimizations
* Embraced by tesseract maintainers as of August 2019

---

<!-- .slide: data-background="https://s3-us-west-1.amazonaws.com/scifindr/articles/images/cephalopods/cephalopods-plate_franz-anthony.jpg" -->

# Standardize!

----

## Why?

* Who knows how `en-default.pyrnn.gz` was trained?
* Synthetic data? Real line images? Both?
* How would `en-default.pyrnn.gz` perform compared to Calamari trained on the same data?
* Engines are evolving :tada: so models must too

----

## Ground Truth


* OCR-D has been developing GT specifications
* Training has different requirements:
  * line-based
  * data integrity is crucial
  * metadata to track provenance
* => Engine-agnostic container format for line GT

----

## Training

* Many parameters equivalent across engines => Common API
* Details matter => JSON Schema
* Track progress and performance uniformly

----

## Evaluation

* Decouple evaluation from training
* Test snapshots of models by predicting GT
* Currently CER and WER
* Synergies with [qurator-spk/dinglehopper](https://github.com/qurator-spk/dinglehopper), [eddieantonio/ocreval](https://github.com/eddieantonio/ocreval) and [impactcentre/ocrevalUAtion](https://github.com/impactcentre/ocrevalUAtion)

---

<!-- .slide: data-background="https://github.com/Doreenruirui/okralact/raw/master/docs/Framework.png" -->
<!-- .slide: class="dark-bg" -->

# Architecture

----

## Caveat

* okralact - the software - is fully working but a prototype
* What we want to push with okralact
  * engine-spanning conventions
  * harmonized network structure specification
  * better documentation and provenance of trainied models

----

## Tech stack

* Redis Queues for training and evaluation
* Different JSON Schemas to model Common API and engine-specifics
* Python/Flask for a simple web interface

----

<!-- .slide: data-background="./okralact-manual.png" -->

---

# Conclusion

* Engine-agnostic training interfaces:
  * possible
  * necessary
  * in everybody's interest

Let's do this!

<img src="https://i.kym-cdn.com/entries/icons/thumb/000/001/987/fyeah.jpg?1269221733"/>

---

### Thank you!

<img src="http://kba.cloud/ocrd-2018-07-11/figures/end-man.png" height="300"/>

* Okralact: https://github.com/OCR-D/okralact
* OCR-D GitHub Org: https://github.com/OCR-D
* OCR-D Specs and Documentation: https://ocr-d.github.io
* Chat with us: https://gitter.im/OCR-D/Lobby

Talk to [@kba](https://github.com/kba), [@cneud](https://github.com/cneud), [@seuretm](https://github.com/seuretm) at HIP/ICDAR!
