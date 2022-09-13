# Developer Documentation for Agile Projects

1. Principles
2. 1Techniques
3. Categories of documentation

## Why this talk?

* Although there is a lot of good material on agile coding techniques and practices, there's very little practical advice on documentation.

* There is a general consensus that developer documentation is "waste" and should be kept to a minimum, with vague guidelines such as:

  - "Just enough" (how much is enough??)
  - "Keep it simple" (what does 'simple' mean?)
  - Eliminate wherever possible (how?!)
  - Use technology (which technology?)

* By contrast, this talks describes a straightforward and practical approach to documenting Agile projects, which is driven by adding value rather than eliminating waste.

## DevDocs are not User Docs

Just to be clear, we are talking about documentation that is internal to a product and not intended for the users of the product. Only the development team will see this documentation.

* It may include:
  - User stories
  - Tasks
  - Bug reports
  - Data dictionary
  - Domain Glossary 

* It will not include:
  - User guide
  - Configuration guide
  - Reference guide
  - Product manual
  - Any stage-gate documentation

## Exception: Development of Software Libraries

* There is one odd case when developer documentation and user documentation seemingly overlaps - _software libraries_.

* For example, you are likely to consider a comprehensive description of the classes and methods of your library to be a deliverable to the end user.

* But this paradox is dissolved as follows: if it is delivered to the customer it is not developer-documentation! It is a deliverable and managed in exactly the same way as the other artefacts - fully under version control, integrated into the user stories, etc.

## Why bother writing DevDocs?

* What's our motivation for writing documents that are not part of the product stream? Isn't that just waste?

* Put simply, no. We need to maintain a sufficient product inventory of formal and informal assets (code, data files, images) that are required for the continued production and maintenance of the product stream, which is ultimately a creative, human process.

* So function of the product inventory is not merely to mechanically build the product over and over again but also to tell the story of what, how and why the assets of the inventory are the way the are and to record the operating procedures. 

* This is necessary to get new developers engaged and up to speed and, as we all know, to jog our own memories after a few months have past.

## Principle: Value/Cost Tradeoff

* This isn't a blank cheque for writing any old documentation. Everything we add to the product inventory needs to be kept up to date, which means its value has to be proportionate to the maintenance cost.

* So we are on the lookout for tools and techniques that reduce the cost of creating documents and, most importantly, keeping them up to date.

* Even automated documentation has a (small) maintenance cost associated with it i.e. the cost of maintaining the automation. 

* Note: There's a useful analogy with maintaining a body of unit tests. Unit tests cost effort to maintain but, over time, pay their way. So the Agile enthusiasts have developed test frameworks and tools that minimise the cost of managing and maintaining unit tests.

## Principle: Self-Describing Assets

* One of the ways to reduce the burden of managing documentation is to interweave the asset content with its description ("meta-content") and synthesize the documentation from the asset. This can be done with a tool or custom script.

* This reduces work in several ways. 
  - It removes the overhead of swapping between a source object and its documentation object.
  - It eliminates the issue of having to cross-check to find out if a source object is documented
  - When altering the source object, it is easy to check the description.
  - The tool/script can insert boilerplate style and cross-references, so they do not have to be manually maintained.
  - The nature of the object being described can often be inferred by the tool/script to provide useful content and navigational elements.
  - Indexes and table-of-contents can be generated automatically.
  - The descriptive content can be utilised by the IDE to provide "Intellisense"

## Principle: Domain-Based Naming (Variables, Methods, Functions, Classes)

* Many of our source assets are quite mathematical in nature and heavily use symbolic names internally.

* Rather than pick opaque "maths-style" names like `x`, `y`, `A` or `B`, we can pick quite descriptive names. So instead of a variable such as `R`, we might use the more descriptive name `distanceFromHome`.

* The names we pick should make it clear how the text corresponds to the business/problem domain. So rather than call a variable "indexIntoArray", which relates to the world of programming, it might be called something like `positionOfApplicantInQueue`.

* When we use names that relate to the business/problem domain (sometimes called "the metaphor"), the source code often makes good sense in both the programming-domain and the business-domain. 

* When used well, this technique can often make other annotations redundant - reducing work still further.


## Technique: Autodocs

* A key technique for keeping costs low is automation.

* Good examples of this are Javadocs and Doxygen. These tools generate detailed, structured API documentation in HTML (etc) from _annotated_ source code. 

* Another good example is Database Notetaker, which generates HTML (etc) from the schema of the database, combining it with annotations that are kept in a separate XML file.


## Technique: Formal Grammars

* A variation on autodocs is to use formal descriptions, typically in XML, JSON or YAML, that can be used to automate consistency checks _and_ to generate human readable documentation.

* A popular and recent tool is Swagger. This describes a REST API in a OpenAPI (JSON) document.

* Another example of reducing the cost of maintenance is the automatic production of railroad diagrams from a EBNF grammar. Tools such as https://pypi.org/project/railroad/ take the easy-to-edit EBNF format and generate the hard-to-edit, visual format of railroad diagram images.

## Technique: Automated Image Generation

* In general, plain text descriptions are easier for programmers to maintain than images. So it can be effective to generate clean visuals from a plain-text "DSL" - sometimes referred to as diagrams as code.

* For example, generating a network diagram from a plain text description is made easy with graphviz. 

* And these DSLs can be useful as intermediate targets for other tools. For example, pydeps builds on graphviz is pydeps to show dependencies between python modules.

* Other similar plain-text tools are blockdiag, Syntrax, erd, state-machine-cat, PlantUML. And there is a wealth of tools that generate output using javascript e.g. Mermaid. 

* Note the pitfall of using lots of tools for your project and finding that keeping a large number of tools working is a maintenance headache.


## Category: Requirements




## Category: Design Documents

## Category: Build & Production Processes

