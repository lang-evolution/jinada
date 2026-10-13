# Project Jinada

## Basic Idea

Take your unit tests to the next level with
sophisticated coverage and modification tracking
that allows you to quickly see where you need
to modify the codebase to get your tests to pass.


## A Modular System

The project is designed for multiple adapters and
is programming language and IDE agnostic.

## Supported Languages and Test Runners

* [ ] Rust
* [ ] Typescript + Jest


## Supported IDEs

Any IDE that supports the language server protocol

## Modification Tracking

Keep track of the last valid AST
where a test still passed.

Do a smart diff of the new AST
vs the working one.
And alert the user to the source of the failing test:

The place in the AST that caused a given test to fail.

Deal with the fact that some lines fix one test, and break another if reverted.

## Coverage Tracking

* Run each test and collect individual code coverage
* "RED" line status - some test failed here
* "GREEN" line status - lines was covered and no failing tests involved
* "GREY" line was never executed during testing


## PoC - VSCode in the browser and a live example for an instant demo


## Data Structures

```typescript

type Span = {
  start: number,
  end: number,
}

type TestRun = {
  testName: string,
  passed: boolean, 
  coverage: { [file: string]: Span[] },
}

// Do not store the entire codebase each run,
// only the initial run stores everything, subsequent runs
// store the items that changed
type TreeSitterASTDiff = 'OPAQUE';

type TestRun = {
  tests: TestRun[],
  sources: { [file: string]: TreeSitterAST }
}

```
## Steps

* Language Detection
* Adapter for Lang X
  * Runs Tests
  * Reads AST of files into TreeSitter struct
* < TODO - intelligent analysis >  
* Language Server Protocol Implementation
  * Creates a feature to view all/failed test list
  * Provides coverage in gutter, and overlay highlighting for
    partial line coverage.
  * Provides a status that displays test status and number
