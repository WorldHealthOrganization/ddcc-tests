# Prototypical Testing Framework for DDCC

This Implementation Guide (IG) demonstrates a prototypical framework for testing conformance to the Digital Documentation of COVID-19 Certificates (DDCC) specification. 

> The tooling here does not qualify or test all aspects of the evolving DDCC specification and is not an authoritative conformance test suite. This IG is not endorsed as the conformance resource for DDCC by the authors, the OpenHIE Community, or the World Health Organization. 

## Objectives

The tooling is meant to provide a basis to understand the reference tooling and how to test their own profiled DDCC frameworks. The tooling also endeavors to provide

* **Reuseable artifacts**: The technical artifacts are meant for reuse by users. Users are encouraged to copy and modify for their own tests and to improve upon the prototypes provided. Permissively licensed tooling is preferred. (If a tool does not have permissive tooling, please file an issue with the authors so a suitable substitution can be found.)

* **Bulk fake data creation**: A method is provided to easily create fake data in bulk based on a template file. This builds on [FHIR Shorthand](https://fshschool.org), an increasingly popular way to author FHIR resources. The data can be used for integration tests, load testing, and QA.

* **Test fixtures based on common tools**: All of the tests are runnable using simple Bash shell scripts and can be modified for Batch files on Windows. The tests using common tools like Postman collections and cURL. Some scripts use Python but are short and the methodology can easily be adapted to other programming languages.

* **Free sandbox for testing using GitHub Actions**: The tests use GitHub Actions which provides free test infrastructure under certain limits. The GitHub Actions workflows can be adapted to other test platforms as they use containers. The GitHub Actions workflows are open source and many may simply be copied into another repository and run on another DDCC-based IG. All tests have short runtimes to stay within the limits imposed by GitHub on free credits. Note that GitHub Actions is only free for public repositories. See the limits [here](https://docs.github.com/en/actions/learn-github-actions/usage-limits-billing-and-administration).

* **Run all tests locally**: The tooling can be run locally on a user's computer using [nektos/act](https://github.com/nektos/act). nektos/act supports Windows, macOS, and Linux. nektos/act makes it possible to test workflows and see how they work instead of having to push to GitHub. 

## Organization

This [tooling](https://github.com/openhie/ddcc-tests) does not contain conformance resources. It only contains documentation and tooling although it is formatted using an FHIR Implementation Guide template for OpenHIE. This is only for constitency as those that are familiar with FHIR IGs may find navigation more familiar.

The IG conformance resources are located at https://github.com/WorldHealthOrganization/ddcc. In some cases, such as for bulk data generation, the IG conformance resources must be cloned locally and run separately, then the tools in this repository run. It is made clear where this is necessary.

## How to Use the Tooling and Testing Framwork

* [**Quick Start**](quickstart.md): This is the starting point to using the tooling using the provided artifacts. This describes the included GitHub Actions which are reusable and should run in any GitHub repository.

* [**Development**](development.md): This is for those that wish to customize and run tests locally.

* [**Fake Data**](fakedata.md): A method is provided to generate fake data based on a template for FHIR Shorthand and neutral names from the periodic table of elements. Data can be generated in bulk with some user modification of the tooling as required for their implementation.

* [**Versioning**](versioning): Versions for reproducing the tests herein.
