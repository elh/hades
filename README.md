# hades

HL7 FHIR terminology server.

A HL7 FHIR facade over [hermes](https://github.com/wardle/hermes), a generic SNOMED CT terminology server. 
The HL7 FHIR specification includes support for a terminology API, including looking up codes and translation. 

Here are some examples of using the FHIR terminology API:

#### Lookup a SNOMED code

http://localhost/fhir/CodeSystem/$lookup?system=http://snomed.info/sct&code=263495000&_format=json
#### Design notes
see https://confluence.ihtsdotools.org/display/FHIR/Implementing+Terminology+Services+with+SNOMED+CT

The operations that will need to be supported are

- $lookup (on CodeSystem resource)  
- $expand (on ValueSet resource) - e.g. ECL, filters
- $subsumes (on CodeSystem resource)
- $closure (on ConceptMap resource)
- $translate (on ConceptMap resource)
- $validate-code (on ValueSet resource)
- $validate-code (on CodeSystem resource)

All of this functionality is obviously available in `hermes` but we need to expose using these
FHIR operations.

I don't believe in loading random value sets into a single terminology server. Rather, these should be decomposed
and recombined as needed. Otherwise, developers solving problems need to coordinate with a central authority 
in order to ensure the value sets and reference data they need are available. The exact choice will be 
determined by the problem-at-hand. Decompose, make them available both as raw data and discrete computing services
that makes using them easy, and then let others compose them together to suit their needs.

