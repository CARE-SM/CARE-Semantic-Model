# Clinical And Registry Entries (CARE) Semantic Model

<p align="center"> 
	<img src="https://raw.githubusercontent.com/CARE-SM/CARE-Semantic-Model/main/images/CARE-SM_logo.png"width="400" height="400"> 
<p align="center" > </p> 
<p align="center"><b>Take CARE of your data!</b></p>
<p align="center"><b>FAIRly!</b></p> 
<hr>

* [What is CARE-SM for](#introduction-to-care-sm)
* [How is CARE-SM born?](#genesis-of-care-sm)
* [What design principles underlie CARE-SM?](#foundational-design-principles-of-care-sm)
    * [Core structure](#core-structure)
    * [List of defined data elements](#list-of-defined-data-elements)
* [Data model implementation](#implementation)
* [Full Documentation](#full-documentation)
* [Communication and feedback](#communication-and-feedback)
* [Cite us](#cite-us)
* [Acknowledgement](#acknowledgement)

<hr>

## Introduction to CARE-SM

Clinical And Registry Entries (CARE-SM) is a semantic data model designed to effectively represent healthcare patient information by using knowledge graphs represented in the Resource Description Framework (RDF). This technical description aims to provide a comprehensive overview of CARE-SM, its origins, and the design principles that underlie its structure.

## Genesis of CARE-SM

CARE-SM is a more robust and matured representation of its precursor, the Common Data Element (CDE) semantic data model. The primary objective of its creation was to develop a semantic data model capable of representing [a set of common data elements for rare diseases registration](https://eu-rd-platform.jrc.ec.europa.eu/sites/default/files/CDS/EU_RD_Platform_CDS_Final.pdf) recommended by the European Commission Joint Research Centre. CARE-SM stands as the matured iteration of this CDE semantic model, extending its capabilities to encompass the representation of all data elements pertinent to patient registries and clinical encounters.

## Foundational Design Principles of CARE-SM

CARE-SM is built upon the [Semanticscience Integrated Ontology (SIO)](https://doi.org/10.1186/2041-1480-5-14) as its core structural schema. SIO is used to define every concept within the data model, utilizing upper-class classes and properties. This knowledge graph serves as an "scaffold" that hold every data element within its structure [Figure 1](#core-structure). By a combination of these instances defined by SIO, it becomes possible to represent every clinical entry comprehensively. 

Moreover, each instance within CARE-SM is associated with a domain-specific ontological class from the [OBO Foundry](http://obofoundry.org/). For instance, the representation of patient birthdate is described at a upper-class level using the ontological term [SIO:attribute](http://semanticscience.org/resource/SIO_000614) and, at a domain-specific level, as [NCIT:Birthdate](http://purl.obolibrary.org/obo/NCIT_C68615). This dual ontological characterization enhances data interoperability and  precise semantic descriptions.


### Core structure

<p align="center"> 
	<img src="https://raw.githubusercontent.com/CARE-SM/CARE-Semantic-Model/main/images/CARE-SM-Core.png"> 
<p align="center"> Figure 1: Core structure </p> 

<hr>
<p align="center"> 
	<img src="https://raw.githubusercontent.com/CARE-SM/CARE-Semantic-Model/main/images/CARE-SM-Schema.png"> 
<p align="center"> Figure 2: Core structure schema </p> 
<hr>


### Context around every data element

In order to keep a common core structure using CARE-SM, only one data element is modeled at a time. For that reason, if you do not have that element, you do not use that particular data representation. This case could lead to situations where data is not aggregated enough. In order to maintain data aggregated when it's necessary, one layer of metadata has been created around every data element representation ([Figure 3](#context-around-every-data-element)). 

Its metadata describes the context of the data represented in the core structure model, giving some temporal information to each data element. This structure is kept even when date/time are the core observation of the model (e.g. date of symptom onset). The context layer creates a timeline of events around every data element. Using this timeline, the model is capable of representing not only individual patient registry entries, but also patient clinical encounters in a precise way.

In addition to the patient's timeline and temporal information, common context _can be_ grouped into other arbitrary data elements by connecting them through event nodes. This event has a common context between data elements, for those cases where more than one data element shares a unique relationship (like conditions/treatment scenarios, visit-based aggregated information). It's not mandatory to implement this in your model, it is merely made possible by this model.

This metadata requires the combination of RDF-Quads and RDF-Triples, rather than only RDF Triple used for regular knowledge graphs. The core structure of the model is represented using RDF-Quad, containing as a fourth element (Quad) the same context ID URL. This URL is used as subject for other RDF Triples that define the metadata layer ([Figure 3](#context-around-every-data-element)).

<p align="center"> 
	<img src="https://raw.githubusercontent.com/CARE-SM/CARE-Semantic-Model/main/images/CARE-SM-Context.png"> 
<p align="center"> Figure 3: Context representation </p> 

<hr>


### List of defined data elements

Based on CARE-SM Core structure, several data element representations can be performed by defining a combination of data model instances, domain-specific ontological terms and its data value. This is a list of data elements presented at patient data registries that can be represented using this data model:

1. Medical history and participation status:
    * [Birthdate](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Birthdate) - Patient date of birth.
    * [Birthyear](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Birthyear) - Year in which a person was born.
    * [Deathdate](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Deathdate) -  Patient date of death.
    * [First confirmed visit](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-First_visit) - Patient first contact with specialized center.
    * [Participation status](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Status) - Patient healthcare participation status.
    * [Symptoms onset](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Symptoms_onset) - Patient signs/symptoms onset.

2. Demographic and questionnaire/PROMs representations:
    * [Sex](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Sex) -  Patient sex at birth.
    * [Education level](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Education) - Patient scholar level code measured by ISCED.
    * [Disability](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Questionnaire-disability) - Patient disability score/assessment.
    * [Questionnaire](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Questionnaire) - Generic questionnaire representation for any clinical question/PROM.

3. Conditions and findings assesments:
    * [Diagnosis](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Diagnosis) - Patient disease diagnosis.
    * [Symptom/phenotype assessment](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Symptom) -  Patient symptom/phenotype assessment.

4. Clinical and molecular measurements:
    * [Laboratory measurement](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Laboratory) - Patient laboratory measurements.
    * [Body measurement](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Body_measurement) - Patient physical measurement of the body. 
    * [Medical imaging](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Imaging) -  Patient medical imaging data.
    * [Genetic variant](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Genotype-variant) -  Genetic variant assessment.
    * [Zygosity](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Genotype-zygosity) -  Zygosity of a certain genetic variant.
    * [Protein variant](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Genotype-Protein) -  Protein variant assessment.
    <!-- * [Aminoacid location](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Genotype-aminoacid) -  Position of a aminoacid in a certain protein chain. -->

5. Treatment-related assesments:
    * [Medication](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Medication) - Patient drug administration based on a prescription.
    * [Surgical intervention](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Surgery) -  Therapeutical interventation related to a surgerical procedure.

6. Research sample availability and consent:
    * [Biobank](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Biobank) - availability of subject's samples in a biobank.
    * [Consent](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Consent) -  consent given by a subject.

7. Clinical trials:
    * [Clinical trial](https://github.com/CARE-SM/CARE-Semantic-Model/wiki/CARE-SM-Clinical_trial) -  patient participation in clinical trial.

## Implementation

This repository is mainly dedicated to present the principles behind the data model and its behavior. To know more about hot to implement it, visit [the implementation repository](https://github.com/CARE-SM/CARE-SM-Implementation).


## Full Documentation
See the [Wiki](https://github.com/CARE-SM/CARE-Semantic-Model/wiki) for full documentation, examples, operational details and other information.

## Communication and feedback
Your feedback is more than welcome. It will help us improve our semantic data model. Please use [github issues](https://github.com/CARE-SM/CARE-Semantic-Model/issues) to provide your feedback.


## Cite us
To cite this model please use this publication [Semantic modeling of common data elements for rare disease registries, and a prototype workflow for their deployment over registry data](https://doi.org/10.1186/s13326-022-00264-6).


## Acknowledgement
This work was done in the [European Joint Programme on Rare Diseases (EJP RD)](https://www.ejprarediseases.org/) project which has received funding from the European Union's Horizon 2020 research and innovation programme under grant agreement N°82557.  
![EU logo](https://github.com/ejp-rd-vp/smart-guidance/blob/main/images/eu-flag.png?raw=true)  


