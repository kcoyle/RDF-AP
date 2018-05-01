# Application Profile over RDF

There are tensions between the idea of application profiles, structured metadata, RDF, and OWL. The intention of the RDF-AP is not to create an AP using RDF, but to use application profiles to provide the structure, rules, and user documentation for metadata that is based on RDF. In addition to that, this project intends to follow the principles of simplicity that are key to the Dublin Core work. 

## RDF as abstract model

RDF is an abstract model that describes a simple unit, the triple. This simple unit is incredibly powerful; it allows one to create anything from simple to very complex data graphs. By itself it does not satisfy some key requirements of metadata such as usage constraints, structural relationships, etc. Some of these functions have been addressed by the OWL2 standard, but the end result of those was not the same as a metadata definition because of some inherent aspects of RDF and in particular OWL. I see these as being differences between structural definition and inferred semantics.

## Structure v. semantics

Both RDF and OWL express semantic relationships that were primarily introduced by the artificial intelligence community. Statements in the AI community are often of the type "A is a type of B" or "Because C, then A is a type of B". Semantics in this sense are logical axioms that can be expressed in graph form. The AI community is interested in being able to say things like:

    SubClassOf( 
      :Grandfather 
      ObjectIntersectionOf( :Man :Parent )
     )

meaning "every Grandfather is both a man and a parent (whereas the converse is not necessarily true)" ([https://www.w3.org/TR/2012/REC-owl2-primer-20121211/ OWL2 Primer])
 
Axioms of this type express knowledge about the world, meaning that they are part of the metadata for a very big universe, the universe of everything. The data that we often call "metadata" has a much more modest goal: metadata describes a carved-out area of knowledge, and often describes things for a particular purpose rather than emphasizing meaning. When you buy a home appliance, there are technical specifications that give relevant information like dimensions, color, and features.
