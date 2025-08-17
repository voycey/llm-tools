# PRD based workflow for coding agents (e.g. Claude 4)

I did this from within Cursor, its codebase indexing capabilities allow the LLM to ask questions in natural language against the codebase to form this better.

## First Steps
--------------

### Scoping
Comprehensively describe the structure of your project, your goals, how specific things should function.
Do this as a step by step implementation approach, if you are implementing this into an existing set of code describe what the existing code does in detail and @tag specific files and folders and paste in configuration items that are relevant.

This list will form the "meat" of the product requirements document (PRD) so it is important that it is extremely detailed - think around the level that a tech BA would produce.
It is important that you instruct it to develop patterns at this point (for example - all contracts between layers should be defined using OpenAPI specifications that are generated at /api/openapi and clients created using this interface only). Its important that you mention any specific design decisions you want to make here too, specifically about how the flow of information works between microservices or how 

Its important that you mention any specific technologies you want to use in the context of the discussion.

This section is the most important part of the process - aim to spend a good amount of time on this, the final list will likely be quite long.

The scope of this part of the document should represent a single large set of features that might be considered an MVP. (Mine is usually around 4 phases each with about 3 tasks.)

### Adding context

*CONTEXT IS EVERYTHING*

LLM's are good at pulling out information but their accuracy isn't always great, I find that not only adding items to Cursors Documentation indexing (e.g. the libraries documentation website) but also including the source code of modules from Github directly into the source tree helps it understand context (be sure to tag these codebases - and especially their README's in as part of the discussion to ensure that the context is non-ambiguous)


### Finish this up with by adding this verbatim at the end of your bulletpoints:

```
Microservices created should all include a start.sh script that starts the relevant services:
Include a --dev parameter that enables autoreload on change for development purposes.
Include a --skip-integration parameter that skips integration tests that would fail due to sequencing.

All steps should include comprehensive tests both unit and integration tests, integration tests that will fail now should be allowed to fail but track these to have the "allow fail" flag removed when the integration test should pass.

IMPORTANT - BEFORE ACTIONING ANY OF THESE STEPS, CREATE DETAILED AND EXPANDED INSTRUCTIONS OF THE WORK TO BE DONE IN AN INSTRUCTIONS.md FILE IN A FOLDER CALLED tasks IN THE ROOT OF THE FOLDER.
THIS SHOULD BE IN THE FORM OF A PRD DOCUMENT AND NEATLY STRUCTURED.

WAIT FOR CONFIRMATION BEFORE MAKING ANY OTHER CODE CHANGES OTHER THAN THE INSTRUCTIONS FILE
```


## Next steps
--------------

Review the PRD document that has been generated, specifically checking for:
1. Sequencing of the phases
2. Coverage of the instructions created (e.g. does it match what you want to build)
3. Correct use of the tools you have specified
- basically review it the same way you would any set of requirements documents, erorrs at this point will be amplified into the future

Iteration:

Inform the LLM of changes that you make to the PRD (it's best to make these changes yourself but you can also iterate using the LLM), you can also ask clarifying questions of it the same as you would to a BA.
Treat this as a technical BA.

Again - this part of the process can take a while, it's important the PRD is accurate and comprehensive.


## Starting "development"
--------------------------

When ready, tell the LLM to start using the following prompt:


```
Lets proceed wtih Phase 1, Task 1.1 only. Do not attempt to proceed past Task 1.1

IMPORTANT: Create an IMPLMENTATION.md that tracks the implementation of the Phases and Tasks in @INSTRUCTIONS.md.

After each item in the task is completed update this IMPLEMENTATION file and describe what was implemented and the specifics of the implementation.
```

## Iteration
--------------

From here it is a process of iteration and code review, review the completed items (Cursors diff is helpful here), make sure that the tests and services run in terminal (the agent should run them in chat but often the execution environments are different) - ensure the test suites run (they will save you down the track).
Fully reviewing and running the code after each task completion is recommended, the LLM *WILL* do things differently than you might, patterns can sometimes be antipatterns or just overly complex

### Committing and using Git
Commit after you have tested and confirmed it to be working.

## Moving on
------------

Basically just repeat the steps under `starting development` and iterate on a task by task basis - dont be tempted to have it create an entire phase at once, it will try and do it and it will write the code but you will completely lose track of how it has done it - keep the cognitive load small enough to reivew.

