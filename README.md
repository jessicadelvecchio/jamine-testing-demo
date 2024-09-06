# [Testing with Jasmine](https://jasmine.github.io/)

Writing tests for our code

## Benefits

- It is worth the time to learn when you begin working with larger code bases/projects. Working with other developers/a team. When functions and services are interacting.
- It is a core skill for professional developers
- Clarify the expectation of a functions
- Helps create documentaion for your code
  - How does your code work?
  - What is the purpose for each section?

## About

Is one of the most popular testing frameworks. It does work with other languages though there are language specific frameworks out there. There are many different testing frameworks that work similarly but they do have their differences.

## Set up

Jasmine can be used standalone or downloaded into your local files.

To add via CDN, add the CSS files to the <head> of html file. Add the 3 JS files to the end of html file. These are to be placed before the files to be tested.

It is best practice to add a separate demo.test.js file to your code. Add this script after the files to be tested.

## Using Jasmine

Testing any possible outcomes of your code saves time in the end. It is possible to easily test `if`/`else` statements, fringe cases and ensure that any errors are thrown in the appropriate circumstances.

Jasmine provides an easy visual for where your code has passed/failed using colors green/red.

The format to test is `expect(someValue).someMatcher()`. There are many different matchers depending on what the expected outcome should be.

`it` is a function that takes two arguments. (1) What the code `"should do..."` so that you know where to look to find the issue to be addressed. This makes looking for issues much easier than looking through lines of code. (2) A callback function that refers back to the function/code to be tested which accepts paramenter to be tested and the expected outcome.

Each `it` function can have mulitple tests within it.

## [Matchers](https://jasmine.github.io/api/edge/matchers)

| Matcher           | Description                                                                                                                                                                                                                                                                         |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.toEqual(obj)`   | Checks that the value is the same (eg, different lists with the same values match). Comparing primitives will behave like `===`, however this matcher cares about values, not references. This checks for deep equality.                                                            |
| `.toBe(obj)`      | Is the same object (eg, different lists with the same values doesn't match). This is exactly like `===`.                                                                                                                                                                            |
| `.toContain(obj)` | Does object/array contain this item?                                                                                                                                                                                                                                                |
| `.not.`           | Will invert the matcher following                                                                                                                                                                                                                                                   |
| `.toThrowError`   | Test that errors are thrown when applicable                                                                                                                                                                                                                                         |
|                   | Tests will automatically fail when run because there are errors being thrown. To test that the errors are working as they should and pass testing, all values within the `expect()` function must be wrapped in their own function. An arrow function works best in such scenarios. |

> > Example of `.toBe` vs `.toEqual`

> `expect(removeDupes([1,1,2,2,3,4])).toBe([1,2,3,4])` Will fail testing because the reference numbers of each array are different.

> `expect(removeDupes([1,1,2,2,3,4])).toEqual([1,2,3,4])` Will pass testing because the comparison is based on values rather than reference numbers.

> > Example of `.toThrowErrow` with arrow functions

> ```
> it("should reject invalid incomes", function () {
>   expect(() => calculateTaxes("lak;jsdf;")).toThrowError();
>   expect(() => calculateTaxes([])).toThrowError();
>   expect(() => calculateTaxes(true)).toThrowError();
> });
> ```

## Describe

Using `describe` allows us to group related tests in the same namespace

## Cleaning up our code after testing

Invoking functions in our code may have undesirable lasting effects: writing to a database or updating HTML of our web app. These hooks allow us to to specify actions to take place before or after each or all of our tests.

Testing libraries typically have some functionality to help us undo the side effects of our tests.

| Hook           | Description                                                                                                                                   |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `beforeEach()` | specifies actions to take place _before each_ test                                                                                            |
| `afterEach()`  | specifies actions to take place _after each_ test                                                                                             |
| `beforeAll()`  | specifies actions to take place _before all_ tests. Good for setting up conditions or initial states of data that we want to use in our tests |
| `afterAll()`   | specifies actions to take place _after all_ tests                                                                                             |

> Example of `afterEach` and `beforeEach`

> Clearing any inputs or values. After each test, we can how to reset our code so there are no lasting effects on our web apps.

> ```
> afterEach(function () {
> ```

    input.value = "";
    usernames = [];

})

## Best practices

Not all code will fit perfectly into any testing category so often a combination of unit and integration tests will be likely.

Most start with writing unit tests to make sure that individual functions are working. From there, writing integration tests to make sure that everything is interacting the way that it should.

### What to test

- Test every function in at least one way
- Think about edge cases
  - What if the list was empty?
  - What about non-integer numbers?
  - What if the file can't be found?
  - Is the first case/last case handled differently?

### Writing testable code

- Write code that is easier to test
  - More functions and smaller functions: easer to test and debug
  - Don't mix logic and UI in a function

### Unit testing

- Tests are arrow in scope
- Used to verify a module of code is doing what it is indended to do
- These are simple and easy to write
- Work well with pure functions. Pure functions do not have side effects on external variables and are easily tested with a simple unit test

> Example of a pure function

```
function append(arr, val){
return [...arr, val]
}
```

### Integration testing

- Tests are broader in scope
- They verify that multiple modules of code are working together
- Are more complex to write and take more time to write
- They work well with impure functions. Impure functions have side effects on external variables. Such as, updating the DOM, writing to a database, etc.

> Example of an impure function

```
function append(arr, val){
arr.push(val)
}
```

## Other notes

One of the example functions uses `Set` and the `...` operator. I had to look them up so here they are for anyone else who may need to know.

A `Set` is a collection of values. A value in a set may only occur once.

The `...` operator makes a shallow copy of JavaScript objects. Instead of using `arr2 = arr1` which would mean that any change to `arr1` would reflect in `arr2`. `...` makes a copy that is completely separate from the original. Changes to one will not reflect on the other.
