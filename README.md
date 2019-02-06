# RDF-AP

This is ongoing work to modify the DC-Description Set Profile, taking into account the vocabularies of ShEx and SHACL.

## DSP vocabulary project
* [Proposed vocabulary](https://github.com/dcmi/dcap/blob/master/schemaList.csv) for profiles
* [DSP ontology](https://github.com/dcmi/dcap/blob/master/dsp.ttl)
* [Diagram](dspDiagram2.jpg) for this vocabulary
* [Diagram with rules](dspDiagram.jpg) proposes a possible way to include more complex rules within the profile
* [Comparison](BIBFRAMEcompare.csv) of the proposed vocabulary with other profile vocabularies, including DSP

## Background on project

### Files

[Patterns](Patterns.md) proposes a basic list of design patterns used for metadata description and validation.

[Requirements](requirements.md) is a list of requirements.

[Use cases](Use_cases.md) is a gathering of use cases relevant to the task.

[Description Set Profile - 2](DSPedited.md) is a re-writing of the DSP document.

### Summary

From 2014 to 2016 a Dublin Core task group met to discuss the requirements for an [application profile for RDF data](https://github.com/dcmi/repository/blob/master/mediawiki_wiki/RDF_Application_Profiles.md). These requirements were input to the W3C RDF validation working group that developed [SHACL](https://www.w3.org/TR/shacl/). RDF validation, however, is not the same as a profile, therefore a suitable "core" of functions for simple application profiles is still needed.

This site is one vision of a simple solution to the needs of metadata developers for a standard application profile definition. It leans toward RDF metadata but could be applied to other solutions. The basic assumption (see the [Requirements](requirements.md) document) is that there are many people designing and employing metadata who do not have either extensive metadata training nor available tools to aid them. In keeping with its history of providing a core vocabulary for metadata, the documents here attempt to define a very basic core vocabulary for the description of metadata profiles.

Many metadata profiles "in the wild" make use of tables (rows and columns) in their documentation. For this reason, this project includes an alignment with the W3C's [tabular metadata](https://www.w3.org/TR/tabular-metadata/) work (also known as CSV on the Web, or CSVW). Such a solution would allow developers to create their metadata as a set of tables, which could then be converted to serializations such as RDF or JSON. These profiles would also support instance data in table form. (Support for non-tabular profiles is not ruled out. This can be considered a first, experimental step using tables as a "low hanging fruit.")

Eventually, it is desirable that metadata profiles be actionable. Part of this would be the ability to transform profile descriptions into validation schemas for the instance data that the profile defines. Thus a profile would generate the code needed to validate instance data that professes to follow that profile. Currently, DCMI is working with the [ShEx](http://shex.io) working group to align the metadata profile proposal with ShEx validation rules.


