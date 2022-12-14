# Developer Documentation for Agile Projects

1. Principles
2. Techniques - the tools that are available
3. Tools/Examples of Techniques
4. What shall we document? And how?

## Why this talk?

* Although there is a lot of good material on agile coding techniques and practices, there's very little practical advice on documentation.

* There is a general consensus that developer documentation is "waste" and should be kept to a minimum, with vague guidelines such as:

  - "Just enough" (how much is enough??)
  - "Keep it simple" (what does 'simple' mean?)
  - "Eliminate wherever possible" (how?!)
  - "Use technology" (which technology?)
  - "Document as late as possible" (how late? actually late?)
  - "Use executable specifications" (why?!)

* By contrast, this talks details a straightforward and practical approach to documenting Agile projects, which is based on adding value rather than eliminating waste.

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

* So the function of the product inventory is not merely to mechanically build the product over and over again but also to tell the story of what, how and why the assets of the inventory are the way the are and to record the operating procedures. 

* This is necessary to get new developers engaged and up to speed and, as we all know, to jog our own memories after a few months have past.

## Principle: Value/Cost Tradeoff

* There is no "blank cheque" for writing any old documentation. Everything we add to the product inventory needs to be kept up to date, which means its value has to be proportionate to the maintenance cost.

* So we are on the lookout for tools and techniques that reduce the cost of creating documents and, most importantly, keeping them up to date.

* Even automated documentation has a (small) maintenance cost associated with it i.e. the cost of maintaining the automation. 

* Note: There's a useful analogy with maintaining a body of unit tests. Unit tests cost effort to maintain but, over time, pay their way. So the Agile enthusiasts have developed test frameworks and tools that minimise the cost of managing and maintaining unit tests.

## Principle: Living, Focussed Documentation

* Although this goes against the instincts of bookish people everywhere, project documents have a shelf-life. 

* A key principle is that only the set of currently useful documents are kept in focus, kept up-to-date and that all others are promptly retired/archived and moved out of focus.

* This goes hand-in-hand with the notion of "living documentation" that is actively maintained by the team.

## Principle: Collaborative Documentation

* To reduce the cost of maintaining documentation, we prefer collaborative media such as Wikis with access that is open to the whole team.

* This eliminates the time and cost overheads of passing updates between developers. If a developer notices that a document needs updating they can do it there and then.

## Principle: Co-versioned Documentation

* A good deal of developer documentation is tied to the version of the code e.g. database schema. When that is the case, its a good idea for it to be incorporated into the source repo.

* When a team maintains multiple versions of a product, each version may require its own copy of the focus set (or sections dedicated to specific versions). 

* Because of rising costs, teams need to make a thoughtful choice as to the contents for non-current version. 
  - Items stored in the repo (or generated by CI) are automatically managed by version.
  - Some items are version independent. 
  - But version dependent info, stored outside the repo, with manual input has extra costs, which degrades the value of that information.

## Principle: JIT Content and Level of Detail (vs AOT)

* How does JIT documentation work? 

* By breaking the monolith up into little pieces that are incrementally created.

* By allowing documentation to start life as rough statements and become refined as time goes on.

## Technique: Use Self-Describing Assets

* One of the ways to reduce the burden of managing documentation is to interweave the asset content with its description ("meta-content") into a single source object.

* We can either synthesize the documentation from the source or even treat it as a replacement for separate document.

* This reduces work in several ways. 
  - It removes the overhead of swapping between a source object and its documentation object.
  - It eliminates the issue of having to cross-check to find out if a source object is documented
  - When altering the source object, it is easy to check the description.
  - The tool/script can insert boilerplate style and cross-references, so they do not have to be manually maintained.
  - The nature of the object being described can often be inferred by the tool/script to provide useful content and navigational elements.
  - Indexes and table-of-contents can be generated automatically.
  - The descriptive content can be utilised by the IDE to provide "Intellisense"

### Example: Autodocs

* A key technique for keeping costs low is automation.

* Good examples of this are Javadocs and Doxygen. These tools generate detailed, structured API documentation in HTML (etc) from _annotated_ source code. 

### Example: Database Documentation

* Another good example is Database Notetaker, which generates HTML (etc) from the schema of the database, combining it with annotations that are kept in a separate XML file.

## Technique: Use Domain-Based Naming (Variables, Methods, Functions, Classes)

* Many of our source assets are quite mathematical in nature and heavily use symbolic names internally.

* Rather than pick opaque "maths-style" names like `x`, `y`, `A` or `B`, we can pick quite descriptive names. So instead of a variable such as `R`, we might use the more descriptive name `distanceFromHome`.

* The names we pick should make it clear how the text corresponds to the business/problem domain. So rather than call a variable "indexIntoArray", which relates to the world of programming, it might be called something like `positionOfApplicantInQueue`.

* When we use names that relate to the business/problem domain (sometimes called "the metaphor"), the source code often makes good sense in both the programming-domain and the business-domain. 

* When used well, this technique can often make other annotations redundant - reducing work still further.



## Technique: Use Formal Notations that can be used for Checking Correctness

* Rather than just describe structure informally in prose, we prefer formal notations that can be utilized as part of CI to validate the build.

* These are often referred to as using 'executable' specifications, which is a misnomer but well-established. (Strictly speaking they can be automatically validated rather than executed.)

* We integrate the checking into the product CI, so that we get early warning that they are out of date (reduces cost, increases value) or that the working prototype has a problem (increases value).

### Example: Acceptance Criteria in Gherkin

* One of the more eye-popping success of the Agile tools revolution is the use of the Gherkin syntax to write acceptance criteria, which can be translated into CI tests that constantly validate the build.

* High cost, high value - Although this involves a good deal of up-front work, it generates a body of very effective user-level tests that can be integrated into CI. Because failures are quickly detected they are much easier to keep up to date and also protect against inadvertant violation.

## Technique: Formal Notations that can be used to Generate Diagrams (etc)

* Another use of formal notations is to produce visual documentation e.g. dependency diagrams, flowcharts etc.

* These are typically easy-to-maintain plain-text representations that tools can turn into very readable documents or diagrams that would otherwise be expensive to keep up to date.

### Example: Swagger, OpenAPI -> Docs

* A popular and recent tool is Swagger. This describes a REST API in a OpenAPI (JSON) document.

### Example: Railroad, EBNF -> Railroad Diagrams

* Another example of reducing the cost of maintenance is the automatic production of railroad diagrams from a EBNF grammar. Tools such as https://pypi.org/project/railroad/ take the easy-to-edit EBNF format and generate the hard-to-edit, visual format of railroad diagram images.

### Example: GraphViz, dot -> Network Diagram

* For example, generating a network diagram from a plain text description is made easy with graphviz. 

### Example: Other tools

* And these plain-text DSLs can also be useful as intermediate targets for other tools. For example, pydeps builds on graphviz to show dependencies between python modules.

* Other similar plain-text tools are blockdiag, Syntrax, erd, state-machine-cat, PlantUML. And there is a wealth of tools that generate output using javascript e.g. Mermaid. 

* Note the pitfall of using lots of tools for your project and finding that keeping a large number of tools working is a maintenance headache.

## Technique: Modular Documentation

* In "Big Up Front" methods, we conceive of documentation as a finished product that is not only fully detailed but has full coverage. The classic "functional specification" would 'ideally' cover every aspect of the planned system in detail.

* To fit in with Agile principles, we flip that around by using modular documentation that allows us to:
  - Partition the document into "pages" or "cards"
  - At ony one time only provide partial coverage, only providing "pages" that have been part of the focus.
  - Have variable the levels of details on different "pages"
  - Continually revise pages as the project progresses.
  - Not enough tags
  - Swimlane support
  - Too few views

### Example: Generic Card-Based Systems - Trello, Restyaboard, Wekan

* TODO - we need to explain the disadvantages of them
  - Poor structured search (querying)
  - No integrated wiki/repo/work-item links
  - Trello has awkward limits on free version


### Example: Wikis

* TODO


### Example: Jira, Azure DevOps, GitHub, Fossil
* TODO

### Example: Other Work-Item Based Systems

* Too numerous to detail ...

* Free (Self-Hosted): Trac, Redmine, Taiga, Gogs, Open Project, Bugzilla, NearBeach

* Paid/Freemium: GitLab, Assembla, Basecamp, Pivotal Tracker, Taiga, Monday.com 

## Technique: Lightweight Markup Languages

* Companies emphasise using corporate templates using popular but complex tools such as Microsoft Word that carry the corporate brand. Such branding is often freighted with multiple serious problems e.g.
  - verbose tables that are almost useless substitutes for change tracking
  - verbose tables for references to other documents
  - poorly controlled table of contents
  - poor stylesheet construction with inadequate support for section hierarchy/numbering
  - poor choice of fonts for on-screen reading (chosen for printed output)
  - low contrast colours
  - tiring white background
  - no consideration given to accessibility

* More problematically, Microsoft Word provides friendly but, for devs used to github or equivalent, comparatively puny support for change management and review.

* Since devdocs are entirely internal and ideally co-versioned, this has led to the adoption of plain-text markup languages that provide minimal styling, excellent syntax highlighting. As we have repeatedly seen, human-friendly plain-text files are managed well by git.
  - embedded in the repo for co-versioning and inclusion in CI
  - minimal styling means less time wasted on getting styling and layout right
  - direct support for hyperlinks
  - plain text editor is adequate tooling
  - plenty of FOSS support

### Example: Markdown

### Example: AsciiDoctor

### Example: ReST


## Category: Build & Production Processes

## Category: Intentions = Requirements and Specifications

## Category: Design = Navigating the Gap between Intention & Implementation

## Category: Case Studies

