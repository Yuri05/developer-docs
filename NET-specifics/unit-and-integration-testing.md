# Unit and Integration Testing

# Introduction


Unit testing is an integral part of our software practices and we to keep the code that we write well covered by tests. Currently Pull Requests are only being accepted if they contain at least one unit test ( with the logical exceptions e.g. a PR containing only package updates ) and the code can be considered well covered by unit tests. We try when possible to implement a Test-Driven-Development (TDD) approach, and specifically for fixing bugs it is strongly suggested to first write a failing test according to the error description and then fix the issue, to ensure the correct and permanent elimination of the bug.


For the C# solutions to write unit tests we are using [NUnit](https://nunit.org/) in combination with [FakeItEasy](https://fakeiteasy.github.io/) to mock object and intercept calls and our own [BDDHelper](https://github.com/Open-Systems-Pharmacology/OSPSuite.BDDHelper) comprising of extensions methods to write and structure unit tests in a Behavior Driven Development manner.

# Test Outline

The abstract class:

We usually create one test class file for every class we want to test. Let's take for example a newly created e.g. `public class NewClass`. When writing the unit tests for it we would start with an abstract class which will be the parent to all the specific test case classes:

```
public abstract class concern_for_NewClass : ContextSpecification<NewClass>
{
    protected override void Context()
    {}
}
```
Please follow this naming convention for the abstract unit test classes of calling them  `concern_for_NewClass` where `NewClass` the class to be tested.

Usually in this abstract class we would define the Context() override and also some protected members that would be common to all the test cases (even if their value would not stay constant for every test case). 

The Context() is the setup of the test, where the environment and necessary objects are created. Functionalities that will be used overall in the test class should be defined and created here. As part of this Context() we could assign the `sut` (System Under Test) - alternatively this could be part of the Because() that we will see in the next segment, specifically in the case that our test case concerns the instantiation of the object. 


Apart from this Context() that would then be called ( and if necessary also overriden) for every test case which inherits from this abstract class, we can also create a GlobalContext() override, where we instantiate resource-heavy objects that are used overall in the test class, since objects in the GlobalContext() are only instantiated once per test class.


# The individual test cases

Continuing with our example, we write an example individual unit test class:

```
public class When_changing_a_NewClass_property_value : concern_for_NewClass
{
    protected override void Context()
    {
        base.Context();
        .
        .
        .
    }

    protected override void Because()
    {
        ...
    }

    [Observation]
    public void should_have_updated_the_value_correctly()
    {
        ...
    }

    [Observation]
    public void should_notify_about_the_change()
    {
        ...
    }
}
```

Please note the convention of naming the unit test classes using complete senteces in lowercase separated with underscores('_') instead of whitespaces. The BDDHelper then replaces the underscores with whitespaces for the test reports. The same naming logic applies to the Observations. Unit test classes usually start with "When_.." and Observations with "should_...". It is important that both the unit test class name as well as the observation fully and correctly describe the behaviour that gets tested and the expected outcome. The lenghth of the name is in this case of no big concern.


# Because()

Instead of packing both the behaviour that leads to a result that we want to test and the assertion of the correct outcome in one code segment, we prefer to seperate those two in a `Because()` function where we have the behaviour that will be tested and an `Observation` that tests the outcome.


# Creation of Objects and Mocking 

It is suggested to avoid mocking as far as possible. I our experience this can lead to a situation where too much mocking results in a green test where the actual functionality is not correct and also to more difficult maintenance. Instead it is generally suggested to create real objects where possible and ideally to use helper functions for this task, in order to make the creation of the real objects reusable and avoid code duplication.

Before writing your own function for the creation of an object, please note that in the DomainHelperForSpecs (probably link to the repository file in github here) there already you can find functions for the creations of many frequently used objects, like e.g. individual or simulation. When writing a function to create an object that could be needed overall in the tests, it is this class exactly that should be extended.

As discussed, to mock objects we use FakeItEasy. On the documentation of the [package](https://fakeiteasy.github.io/) you can find a quite detailed description. Still we will present here some of the functionalities that we use more often:

- creating a simple fake objects
fake object calls can be intercepted
A.CallTo.returns  blah blah
in order to return specific objects


# BDDHelper

as discussed Behavior Driven Development manner(only if it really makes sense to elaborate.). It is strongly suggested to use the hereby available functionalities instead of simple NUnit(??????) Asserts for example, for connsistency, but also because some things are centrally documeted in these functions (like comparison tolerance for values for example)  


# Integration Tests

We use integration tests to test functionality that requires the loading of resource-heavy real objects and are generally oriented towards scenarios that run longer, open whole projects, load the whole context etc. There is also a difference in how we handle integration tests compared to normal unit tests in our Continuous Integration pipeline (AppVeyor)  --- possibly a link to our appveyor space????. Unit tests are run on every build, but integration tests are only run on the nightly builds since they are regarded as more time- and resource- consuming.

Here we have the ContextForIntegration (if there are any further structural differences in code we should check)

# Constants for Tests

In order not to fill up the constant definitions that are used for the actuall application, constants used only for tests should be defined in the dedicated classes ConstantsForSpecs(this actually contains very few strings) and PKSIM::: (MoBi?????). 