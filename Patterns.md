
* property cardinality (if not already defined in relationship patterns)
* property value rules

## Entity/entity relationships

* Dependency: 
  * if A then B / if A then not B
  * if A then (pattern), e.g. if A then (B or C), if A then (B and (C or D)), etc.
* Choice
  * one of (list), not one of (list)

## Entity/property relationships

* Dependency
  * if E1 then P1, if E1 then (patterns of P)
* Choice
  * one of (list), not one of (list)

## Property/property relationships

* Dependency: 
  * if A then B / if A then not B
  * if A then (pattern), e.g. if A then (B or C), if A then (B and (C or D)), etc.
  * value of A / relationship / value of B (greater than, less than, equal to)
* Choice
  * one of (list), not one of (list)
* Compound
  * A and B must both be present

## Property/value relationships

There will be many tests that can be done on property values, including ones with dependencies and choices. Some are enumerated here.

| Property value | must/must not|
| -------------- | ------------ |
| value type |  |
| value list (choice) |  |
| value pattern (regex) |  |

## Value/value relationships

* greater than/less than
  * birth date must be less than death date

## Open/Closed

The overall validation may require that the rules be closed, that is, that only the entities and properties in the Application Profile may be present. The presence of other entities or properties will be flagged as an error. [There will need to be a default of either open or closed that can be over-ridden.]
