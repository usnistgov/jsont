# jsont

a python module for JSON Transformations.

Please note that development has halted on this package; see
Background for details.

## Background

This package, developed by Raymond Plante (raymond.plante@nist.gov),
came out of work on metadata development for the Materials Genome
Initiative (MGI) at NIST.  In an effort to develop metadata formats
simultaneously in XML and JSON, the author was interested in have a
tool for JSON data transformations analogous to XML transformations
provided by XSLT.

At the time, there appeared to be very few options for JSON
transformations apart from the jq tool.  Initially, the author thought
jq was inadequate for his purposes primarily for two reasons.  First,
the "stylesheets" used a custom syntax that could not be readily
validated independently of applying it to appropriate input data; in
contrast, a stylesheet expressed in JSON (or in a syntax that was
easily converted to JSON) could readily be validated.  Further,
because stylesheets could not be validated, it would be harder to use
jq to product standard transformations.  Second, he (incorrectly, in
hindsight) felt the module framework was not rich enough to build a
sufficiently complex library of transformations.  Other minor
disadvantages included that jq was implemented in C; a pure-python
implementation would make for easier integration with other pure-python
tools.  

Thus, the author embarked on an effort to prototype a JSON
transformation Python package called jsont.  This work was carried out
initially within the GitHub repository, usnistgov/mgi-resmd 
(https://github.com/usnistgov/mgi-resmd).  Some features of the
approach included:
  * A core stylesheet format encoded in JSON whose syntax could be
    defined via JSON Schema.
  * Alternate stylesheets optimized for ease of authoring which could
    be easily converted to JSON
  * A processing model for applying JSON stylesheets that could be
    standardized: that is, it could be described in a document to
    enable implementation in multiple languages
  * a module system that included standard transforms and a module
    specifically for converting JSON to XML.  
  * user-defined transformations and modules
  * use of JSON Pointer for pointing to and extracting JSON data

Once the author reached the point of demonstrating deep, hierarchical
JSON-to-XML conversion and, thus, understanding better the problem he
was trying to solve, he had a closer look at jq.  He found that he
could replicate all of the capabilities in jsont implemented thus far
in jq, including an XML module.  Furthermore, there were capabilities
still needed to be added to jsont that already existed in jq.  

Given his now better understanding of the problem and of jq, he
decided that its lack of validation and its C implementation were
minor compared to the advantages of a highly capable and widely-used
transformation tool.  Thus, he abandoned development on jsont.  To
preserve the work to-date, the jsont python package was extracted out of
the usnistgov/mgi-resmd repository and into its own usnistgov/jsont
repository.  Please see usnistgov/mgi-resmd for jq-based modules and
scripts for JSON transformation.  

## Dependencies

This package has the following dependencies:

   * python 2.7.x  (python 3.x not yet supported)
   * jsonschema 2.5.x or later
   * jsonspec 0.9.16 or later

In addition, the testing framework uses py.test. 

## Running Tests

The included tests apply unit-tests to the tool code and scripts.
Tests also check the correctness of the schemas and examples.  

Currently, tests only exist for the JSON schemas, examples, and
tools.  py.test is used to execute these tests.   To run, change into
the root directory of this distribution and type "py.test".  

