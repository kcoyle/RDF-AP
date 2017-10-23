


# Description set profile, RDF version

A description set profile is a document that describes the components of a metadata profile: the *things* the metadata describes, the terms it uses to describe those, the allowed values for the terms, rules relating to the values and terms, and human-readable documentation that guides the creation of valid metadata.

# Description Set

A description set is a document with one or more descriptions.

# Description

A description describes a single resource; that resource is identified with an IRI.

## Standalone

**Summary**

Whether descriptions matching this template are allowed to occur standalone, i.e. without being the value of a property. 

**Allowed values**

"yes" / "no" (xsd:boolean)

**Default**

none

**Conditions**

If standalone is "yes", a matching description may not be a description of value occurring elsewhere in the DSP. 

If standalone is "no", a matching description *must* be a description of value occurring elsewhere in the DSP. 

If standalone is not defined, then the description set is silent on this issue.

If this description template is referred to in a Value Constraint, standalone cannot be "yes".

**Label**

standalone

## Minimum occurrence constraint

**Summary**

The minimum number of times this kind of description must appear in the Description Set.

**Allowed values**

non-negative integer

**Default**

0

**Conditions**

must be equal or less than the Maximum occurrence

**Label**

minOccurs

## Has statement

**Summary**

Relationship of a description to its statement(s). 

**Allowed values**

IRI of a statement

**Default**

none

**Conditions**

There SHOULD be at least one statement associated with each description. There is no limit on the number of statements.

**Label**

hasStatement

## Resource Class Membership Constraint

**Summary**

Classes that the resource may be an instance of

**Allowed values**

a list of class URIs

**Default**

none

**Conditions**

if given, the resource must be an instance of one of the given classes. If this property is not used, there is no constraint on the what classes the description may be an instance of

**Label**

resourceClass

## Maximum occurrence constraint

**Summary**

The maximum number of times this kind of description is allowed to appear in the Description Set.

**Allowed values**

non-negative integer or "infinity"

**Default**

"infinity"

**Conditions**

must be equal or greater than the Minimum occurrence

**Label**

maxOccurs

# Statement

A statement is a single data element that is used in the metadata to describe the resource that is identified in the description. A statement is identified with the IRI of an RDF vocabulary term. Statements are associated with/members of a description with the _hasStatement_ property. The statement defines the valid values for the vocabulary term, and other constraints.

There are no limits on the number of statements that can be associated with a description. A description with no statements is not actionable.

__Questions: __

__ 1. Can the same property be associated with more than one statement? __

__ 2. Can there be properties that are not associated with a statement? (No) __

A statement template has the following possible constraints.

**Label**

Each statement has either an rdf:label property, or a label property from another vocabulary, such as SKOS. 

__Issue: should labels from the original vocabulary be used if no label is given in the description set?__

## Minimum occurrence constraint

**Summary**

The minimum number of times this kind of statement must appear in the enclosing Description. If the value of this property is zero ("0"), the this statement is not required. 

**Allowed values**

non-negative integer

**Default**

0

**Conditions**

must be equal or less than the Maximum occurrence

**Label**

minOccurs

## Maximum occurrence constraint

**Summary**

The maximum number of times this kind of statement is allowed to appear in the enclosing Description. If the value of this property is greater than one, then this property is repeatable. If no maxOccurs property is included in the profile, then the property is repeatable and there are no limits on how many times it can be repeated.

**Allowed values**

non-negative integer

**Default**

none

**Conditions**

must be equal or greater than the Minimum occurrence

**Label**

maxOccurs

## Value type constraint

**Summary**

The type of value that is allowed in this Statement.

**Allowed values**

__Should this use object/data from OWL?__

__Would it be useful here to indicate that the value is a value list?__

**Default**

none

**Conditions**

If not provided, there can be no constraints on the value. _Same as OWL annotation property._

**Label**

valueType

Note: that the value type constraint should not contradict the range given for the used properties where they are originally defined.

## Value constraints

There are two ways of constraining the property value in a statement: 

* By giving an explicit list of allowed properties

* By requiring the property to be a sub-property of a given property.

Exactly one of the above methods must be used in a single statement template.

### Value list constraint

**Summary**

A set of properties that are allowed in this statement template.

**Allowed values**

a list of property URIs

**Default**

N/A

**Conditions**

cannot occur together with a sub-property constraint

**Label**

Property

### Sub-property constraint

**Summary**

Only sub-properties of the given property are allowed in this statement template. Note that the given property is included in this list (all properties are sub-properties of themselves).

**Allowed values**

a property URI

**Default**

N/A

**Conditions**

cannot occur together with a property list constraint

**Label**

SubPropertyOf

## Literal value constraints

Constrains a literal value surrogate in a statement. Only allowed in the case that the type constraint has the value "literal".

**Label**

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

**Label**

LiteralOption

### Literal language constraint

**Summary**

Whether languages are allowed for the literal

**Allowed values**

"mandatory" / "optional" / "disallowed"

**Default**

"optional"

**Conditions**

if "mandatory", Syntax encoding schemes are automatically disallowed.

**Label**

LanguageOccurrence

### Literal language list constraint

**Summary**

Languages allowed for the literal

**Allowed values**

a list consisting of language tags

**Default**

no constraint

**Label**

Language

### Syntax Encoding Scheme constraint

**Summary**

Whether Syntax Encoding Scheme are allowed for the literal

**Allowed values**

"mandatory" / "optional" / "disallowed"

**Default**

"optional"

**Conditions**

if "mandatory", language tags are automatically disallowed.

**Label**

SyntaxEncodingSchemeOccurrence

### Syntax Encoding Scheme list constraint

**Summary**

Syntax encoding schemes allowed for the literal

**Allowed values**

a list consisting of syntax encoding scheme URIs

**Default**

no constraint

**Label**

SyntaxEncodingScheme

## Non-literal value constraints

Constrains the value surrogate in a statement. Only allowed in the case that the type constraint has the value "nonliteral".

**Label**

NonLiteralConstraint

### Description template reference

**Summary**

A reference to a description template that may be used to describe the value

**Allowed values**

an identifier defined in a Description Template

**Default**

Related description not allowed

**Conditions**

if given, any related description of the value within the record must match the referenced Description Template. If the referenced Description Template contains mandatory Statement templates, such a description of the value must exist.

**Label**

descriptionTemplateRef

### Class membership constraint

**Summary**

Classes that the value may be an instance of

**Allowed values**

a list of class URIs

**Default**

no constraint

**Conditions**

if given, the value must be an instance of one of the given classes.

**Label**

ValueClass

Note: this is not a syntactic constraint, and as such might not be evaluated by all processors. If a type statement is desired, an explicit Statement template in a Description Template for the value resource should be created.

### Value URI constraint

#### Value URI occurrence constraint

**Summary**

Whether a value URI must be given

**Allowed values**

"disallowed" / "optional" / "mandatory"

**Default**

"optional"

**Conditions**

**Label**

ValueURIOccurrence

#### Value URI list constraint

**Summary**

URIs that are allowed as value URIs.

**Allowed values**

a list of URIs

**Default**

no constraint

**Conditions**

If a value URI is given, it must be taken from this list. Cannot be specified if value occurrence is "disallowed"

**Label**

ValueURI

### Vocabulary encoding scheme constraint

#### Vocabulary encoding scheme occurrence constraint

**Summary**

Whether a vocabulary encoding scheme must be given

**Allowed values**

"disallowed" / "optional" / "mandatory"

**Default**

"optional"

**Conditions**

**Label**

VocabularyEncodingSchemeOccurrence

#### Vocabulary encoding scheme list constraint

**Summary**

URIs that are allowed as Vocabulary Encoding schemes.

**Allowed values**

a list of URIs

**Default**

no constraint

**Conditions**

If a vocabulary encoding scheme is given, it must be taken from this list. Cannot be specified if vocabulary encoding scheme occurrence is "disallowed"

**Label**

VocabularyEncodingScheme

### Value String Constraints

If at least one value string constraint is given, any value string must match at least one of the constraints. If no value string constraint is given, any value string is allowed.

For each value string constraint, the following may be specified.

**Label**

ValueStringConstraint

#### Minimum occurrence constraint

**Summary**

The minimum number of times this kind of value string must appear in the enclosing Statement.

**Allowed values**

non-negative integer

**Default**

0

**Conditions**

must be equal or less than the Maximum occurrence

**Label**

minOccurs

#### Maximum occurrence constraint

**Summary**

The maximum number of times this kind of value string is allowed to appear in the enclosing Statement.

**Allowed values**

non-negative integer or "infinity"

**Default**

"infinity"

**Conditions**

must be equal or greater than the Minimum occurrence

**Label**

maxOccurs

#### Other constraints

All Literal value constraints (section 6.5) can be used for value strings as well.
