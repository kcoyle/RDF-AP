# Description set

# Description Templates

A description Template has the following attributes.



<del>Identifier

**Summary**

A string that can be used in a Value Constraint to reference a description template that applies to the value resource.

****Allowed values****

A valid XML ID string.

****Default****

N/A

****Label****

ID</del>

_Comment: a separate identifier is not necessary. The description will have a URL as its identifier, as will statements._

## Standalone

**Summary**

Whether descriptions matching this template are allowed to occur standalone, i.e. without being the value of a property.

**Allowed values**

"yes" / "no" / "both"

**Default**

"both"

**Conditions**

If standalone is "yes", a matching description may not be a description of value occurring elsewhere in the DSP. 

If standalone is "no", a matching description *must* be a description of value occurring elsewhere in the DSP. 

If standalone is "both", both are allowed. 

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

## Resource Class Membership Constraint

**Summary**

Classes that the resource may be an instance of

**Allowed values**

a list of class URIs

**Default**

no constraint

**Conditions**

if given, the resource must be an instance of one of the given classes.

**Label**

ResourceClass

# Statement templates

A statement template has the following possible constraints.

**Label**

StatementTemplate

## Minimum occurrence constraint

**Summary**

The minimum number of times this kind of statement must appear in the enclosing Description.

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

The maximum number of times this kind of statement is allowed to appear in the enclosing Description.

**Allowed values**

non-negative integer or "infinity"

**Default**

"infinity"

**Conditions**

must be equal or greater than the Minimum occurrence

**Label**

maxOccurs

## Type constraint

**Summary**

The type of value surrogate (literal/non-literal) that is allowed in this Statement.

**Allowed values**

"literal" / "nonliteral"

**Default**

both allowed

**Conditions**

If no value is given, no further constraining on the value surrogate can be made.

**Label**

type

Note: that the type constraint should follow any range given for the used properties.

## Property constraints

There are two ways of constraining the property in a statement: - By giving an explicit list of allowed properties

By requiring the property to be a sub-property of a given property.

Exactly one of the above methods must be used in a single statement template.

### Property list constraint

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
