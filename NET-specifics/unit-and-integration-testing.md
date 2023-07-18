# Unit and Integration Testing

# Introduction


Unit testing is an integral part of our software practices and we to keep the code that we write well covered by tests. Currently Pull Requests are only being accepted if they contain at least one unit test ( with the logical exceptions e.g. a PR containing only package updates ) and the code can be considered well covered by unit tests. We try when possible to implement a Test-Driven-Development (TDD) approach, and specifically for fixing bugs it is strongly suggested to first write a failing test according to the error description and then fix the issue, to ensure the correct and permanent elimination of the bug.


For the C# solutions to write unit tests we are using [NUnit](https://nunit.org/) in combination with [FakeItEasy](https://fakeiteasy.github.io/) to mock object and intercept calls and our own [BDDHelper](https://github.com/Open-Systems-Pharmacology/OSPSuite.BDDHelper) comprising of extensions methods to write and structure unit tests in a Behavior Driven Development manner.
