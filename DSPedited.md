


# Description set profile, RDF version

A description set profile is a document that describes the components of a metadata profile: the *things* the metadata describes, the terms it uses to describe those, the allowed values for the terms, rules relating to the values and terms, and human-readable documentation that guides the creation of valid metadata.

# Description Set

A description set is a document with one or more descriptions. The IRI of the description set identifies a single resource that may be described with multiple component descriptions, such as journal article metadata that has separate but linked descriptions for the text, the persons who authored the text, and the publisher responsible for publication.

##Administrative

**Comment**

_Probably more administrative information is desired, including: creators, license terms for re-use. I have included Version because that seems to be a universal need. I don't know what else is essential, or if we can push this off to a vocabulary like VOID._ 

## Topic

**Summary**

Topic areas covered by the metadata, such as "documents", "weather data", etc.

**Comment**

_This is needed for discoverability. It could use dct:subject, or it could be done as a schema.org statement if the final document is in HTML. Probably we cannot work this out until we have a better idea of what the form (or forms) of DSP2 will be._

**Allowed values**

Ideally taken from a controlled list. Could be text or an IRI. If an IRI a label should be included for discoverability. Text can be provided as a comma-delimited string.

**Default**

none

**Conditions**

none

**Name**

topic

## Version

**Summary**

The version of the DSP2 document.

**Allowed values**

Any text

**Conditions**

None

**Name**

version

## Version date

**summary**

The date of the version of the document in a standard date form: YYYYMMDD, YYYYMM, YYYY

**Allowed values**

Must be a valid date. 

**Conditions**

none

**Name**

versionDate

# Description

A description describes a single resource; that resource is identified with an IRI.

**Comment**

_I always thought of the descriptions as entities, but could a description be simply a set of properties that don't define an entity per se, such as a group of administrative properties?_

## Standalone

**Summary**

Whether descriptions matching this template are allowed to occur standalone, i.e. without being the value of a property. 

**Comment**

_It would be good to have an example of a situation where this is essential. It seems that with graphs this could be too restrictive. Also this probably requires more validation logic than we can handle here._

**Allowed values**

"yes" / "no" / "either"

**Default**

none

**Conditions**

If standalone is "yes", a matching description may not be a description of value occurring elsewhere in the DSP. The description must "stand alone".  

If standalone is "no", a matching description *must* be a description of value occurring elsewhere in the DSP. 

If standalone is "either" then the description can be used either alone or as a value. 

If standalone is not defined, then the description set is silent on this issue, which has the same affect as "either". 

If this description template is referred to in a Value Constraint, standalone cannot be "yes".

**Name**

standalone

## Minimum occurrence constraint

**Summary**

The minimum number of times this kind of description must appear in the Description Set.

**Allowed values**

non-negative integer

**Default**

0

If undefined, no minimum is enforced. Description is optional. 

Any positive integer means the description is required for the resource identified by the description set. 

**Conditions**

Must be equal or less than the Maximum occurrence

**Name**

minOccurs

## Maximum occurrence constraint

**Summary**

The maximum number of times this kind of description is allowed to appear in the Description Set.

**Comment**

_It may not be possible to use "infinity" if this is defined as datatype non-negative integer. Instead, if no maximum is given, no constraint is assumed (which = infinity)__

**Allowed values**

non-negative integer or "infinity"

**Default**

<del>"infinity"</del>

**Conditions**

Must be equal or greater than the Minimum occurrence. If there is no maximum to enforce, this constraint must not be included in the set.

**Name**

maxOccurs

## Resource Class Membership Constraint

**Summary**

Classes that the resource may be an instance of

**Allowed values**

a list of class URIs

**Default**

none

**Conditions**

if given, the resource must be an instance of one of the given classes. If this property is not used, there is no constraint on the what classes the description may be an instance of

_Not clear why "resource" is used here. Until now this has been called a description. It might make sense to use resource, but we would have to do that throughout. Or we could talk about a "resource description"._

**Name**

resourceClass

## Has statement

**Summary**

Relationship of a description to its statement(s). 

**Allowed values**

IRI of a statement

**Default**

none

**Conditions**

There SHOULD be at least one statement associated with each description. There is no limit on the number of statements. 

**Name**

hasStatement

# Statement

A statement is a single data element that is used in the metadata to describe the resource that is identified in the description. A statement is identified with the IRI of an RDF vocabulary term. Statements are associated with/members of a description with the _hasStatement_ property. The statement defines the valid values for the vocabulary term, and other constraints.

There are no limits on the number of statements that can be associated with a description. A description with no statements is not actionable.

A statement template has the following possible constraints.

**Comment**

_Questions on this_

_1. Can the same property be associated with more than one statement?_

_2. Can there be properties that are not associated with a statement?_

**Name**

Each statement has either an rdf:label property, or a label property from another vocabulary, such as SKOS. 

_Issue: should labels from the original vocabulary be used if no label is given in the description set?_

## Minimum occurrence constraint

**Summary**

The minimum number of times this kind of statement must appear in the enclosing Description. If the value of this property is zero ("0"), the this statement is not required. 

**Allowed values**

non-negative integer

**Default**

0

**Conditions**

must be equal or less than the Maximum occurrence

**Name**

minOccurs

## Maximum occurrence constraint

**Summary**

The maximum number of times this kind of statement is allowed to appear in the enclosing Description. If the value of this property is greater than one, then this property is repeatable. If no maxOccurs property is included in the profile, then the property is repeatable and there are no limits on how many times it can be repeated.

**Comment**

_It may not be possible to use "infinity" if this is defined as datatype non-negative integer. Instead, if no maximum is given, no constraint is assumed (which = infinity)__

**Allowed values**

non-negative integer

**Default**

none

**Conditions**

must be equal or greater than the Minimum occurrence

**Name**

maxOccurs

# Value constraints

## Value type constraint

**Summary**

The type of value that is allowed in this Statement.

**Allowed values**

<deL>"literal" / "nonliteral"</del>
"Object" (IRI) / "Datatype" (xsd:)/ "literal" ()

**Comment**

_The original values of literal and nonliteral followed the DCAM, and the constraints were based on DCAM notions of value surrogates. To move away from that, should this use object/data from OWL?_

_Would it be useful here to indicate that the value is a value list?_

**Default**

If undefined, no further value constraints are applied.

**Conditions**

If not provided, there can be no constraints on the value. _Same as OWL annotation property._

**Name**

valueType

Note: that the value type constraint should not contradict the range given for the used properties where they are originally defined.


## Object constraints

Object values are always IRIs. IRIs can be complete or can be patterns that include the domain, domain name, or some portion of the IRI path.

e.g.s

http://id.loc.gov/authorities/names*  ##limited to name authority list

http://id.loc.gov/authorities/* ##limited to any LC authority list

http://id.loc.gov/ ## limited to any LC IRIs at id.loc.gov

http://.gov/ ## allows any IRI from the .gov domain

Note that a DSP Description can be the value of an object statement. 

### IRI list constraint

**Summary**

IRIs that are allowed as values.

**Allowed values**

a list of IRIs that can be used as values. The list can also contain IRI "stubs" giving at least the

**Default**

no constraint

**Conditions**

none

**Name**

IRIList

### Unique IRI constraint

**Summary**

For a given property, an IRI can appear only once

**Allowed values**

Yes / No

**Default**

no constraint

**Conditions**

_This requires comparing values for some set of properties. This gets into complex validation because it looks at more than one property._

**Name**

UniqueIRI

## Literal value constraints 

Constrains a literal value in a statement. Only allowed in the case that the type constraint has the value "literal".

**Comment**

_This can be a heading, but not sure that we need a property. We'll need to decide this after we model the RDF._

**Name**

LiteralConstraint

### Literal list constraint

**Summary**

Literals that are allowed as values.

**Allowed values**

a list of literals, i.e. (string, language tag) or (string, syntax encoding scheme URI) pairs.

**Default**

no constraint

**Conditions**

if given, no other literal constraint may be given

**Name**

literalList

### Literal maximum length constraint

**Summary**

The maximum allowed length of the literal in bytes

**Allowed values**

non-negative integer

**Default**

no constraint

**Conditions**

Maximum length must be greater than or equal to minimum length

**Name**

literalMaxLength

### Literal minimum length constraint

**Summary**

The minimum allowed length of the literal in bytes

**Allowed values**

non-negative integer

**Default**

no constraint

**Conditions**

Minimum length must be less than or equal to maximum length

**Name**

literalMinLength

### Language tag constraint

**Summary**

Whether languages are required for the literal

**Comment**

_For validation purposes, the values seem to be yes/no, and optional is that this property is not included. But the difficulty is where there is no constraint but a set of valid language codes is given. That could be difficult to express as a validation statement._

**Allowed values**

"mandatory" / "optional" / "disallowed"

**Default**

"optional"

**Conditions**

_(DCAM: if "mandatory", Syntax encoding schemes are automatically disallowed.)(Drop?)_

**Name**

languageTag

### Unique language constraint

**Summary**

For a given property, only one string can appear per language tag. 

**Allowed values**

Yes / No

**Default**

no constraint

**Conditions**

_This requires comparing values for some set of properties. This gets into complex validation because it looks at more than one property. It fulfills some SKOS requirements._

**Name**

UniqueIRI

### Language list constraint

**Summary**

Languages allowed for the literal. The language tag must be one of the tags 

**Comment**

_What is the format of the list? An RDF list? A comma-delimited list? Do the strings need to be in quotes: "@en","@de"? or @en,@de?_

_Can be tested with SHACL:languageIn. Language-tagged strings are defined as type http://www.w3.org/1999/02/22-rdf-syntax-ns#langString._

_there also needs to be a constraint on each language can appear only once_

**Allowed values**

a list consisting of language tags (@xx).

**Default**

no constraint

**Conditions**

This should only apply if languageTag is not "disallowed".

**Name**

validLanguageList




### Datatype constraint

**Summary**

The datatype that is valid for this property

**Allowed values**

An xsd: datatype

**Default**

"optional"

**Conditions**

must be valid xsd: datatypes

**Name**

dataType

### Datatype list constraint

**Summary**

A list of xsd: datatypes that are valid for this property

**Allowed values**

a list consisting of xsd: datatypes

**Default**

no constraint

**Conditions**

Must be valid xsd: datatypes

**Name**

dataTypeList

### Datatype value constraint

**Summary**

Constraints on the actual values, such as "date must be > 1990"

**Comment**

_This is something the validation languages can do. It isn't clear if there can be a simple form of this, but it is a common need._

**Allowed values**

text describing the desired constraints

**Default**

no constraint

**Conditions**



**Name**

dataTypeValue

