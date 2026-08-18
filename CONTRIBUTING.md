# Contributing to `movie-recommender`

To start, thank you for considering contributing to this project. Having contributors such as yourself allow us to develop our website further, and to a high quality, which is very appreciated.

## Getting Started
To begin, please look through our [Code of Conduct](https://github.com/fn5-310/movie-recommender/blob/main/CODE_OF_CONDUCT.md) if you haven't already, to understand the behaviour we are looking to cultivate in our community.

Furthermore, also refer to the [README.md](README.md) for the initial setup instructions for running the project - this is also required to work on the project.

## Contribution Model

## Code Editor
We recommend using an IDE such as [VSCode](https://code.visualstudio.com/) to work on the project for linting and syntax validation.

Regarding IDE extensions, we heavily recommend using [SonarLint](https://www.sonarsource.com/products/sonarqube/ide/) to ensure code is of a high quality and free of any potential security vulnerabilities.

## Architecture Overview
The project is split into two folders, the `client/` and `server/`. Both run on different ports on the dev server, and uses CORS to interact between them.

The `client/` relates to the frontend, utilising React Components and CSS. There is an api folder for an api fetch call onto the backend.

The `server/` relates to the backend, utilising ExpressJS. Because this project utilises TMDB, this mostly pertains to sending get requests and processing the response data. Currently MongoDB is not utilised in the project.

## Filing a Bug Report
If a bug is found, please [submit an issue](https://github.com/fn5-310/movie-recommender/issues/new) on GitHub. When prompted for a template, select `Bug Report` and fill out the fields as required.

Once submitted, a team member will approve the message, or comment/discuss the bug in further detail. After this, you can develop a solution and submit a pull request with the fix.

## Filing a Feature Request
Similar to above, for any feature request or improvement, please [submit an issue](https://github.com/fn5-310/movie-recommender/issues/new), using the `Feature Request` template.

Like the bug report, please wait for approval from a team member before developing any feature, in the case that the feature is being currently developed, out of project scope, or any other reason.

## Changing Documentation
For any changes required to the documentation, a similar process also follows. There is an issue template, `Documentation Modification`, which should be filled out and can be developed once approved, or assigned to a different team member if the scope is sufficiently small. 

## Key Tasks
Issues denoted as key tasks are those that were outlined in the Project Proposal in the initial ideation phase of the project. These tasks are automatically approved to be worked on, and can be worked on once assigned, to prevent overlapping with another contributor.

## Creating a Pull Request
Before making a pull request, ensure that:
- Your branch is rebased to the latest version of `main`
- If your change involves code, that there are corresponding test cases created
- The project can build without errors or crashes

When submitting a pull request, there will be a preset template to fill out, including a checklist of all of the prerequisites before submitting the pull request. The other important section is linking your PR to the issue your PR closes, using closing keywords.

After submitting, a team member will review your work, request changes, and approve your PR. Your PR should then be (if you are merging) squash merged into the `main` branch.

Congratulations! You have successfully contributed to the `movie-recommender` project!

## Creating Tests
`vitest` is used for all test cases, and roughly follows the below structure:

```js
describe("TestSuiteName", () => {
    it("TestCaseName", async () => { // may not be async depending on test type
        const result = testFunction(arg1, arg2);
        expect(result).toBe(`${arg1}-${arg2}`) // toBe checks identity of result and string - use toEqual for equality
    })
    it("TestCaseName2", async () => {
        const result = testFunction(arg1);
        expect(result).toBe(`${arg1}-${arg1}`)
    })
})
```
Given the above structure, each `it()` call makes one test case, while describe groups these tests together.

The test file for a function should be in the same folder as the file being tested, appending `.spec` before the file extension, e.g. `client/testFunction.ts` will have a test file `client/testFunction.spec.ts`.

To run tests:
```
npm run test
```

### Frontend
Frontend tests make use of the react testing library, and work by emulating a DOM and rendering the components used.

Unit testing should be done per component or function file in isolation. These test whether the component or function by itself has all required functionality.

Integration testing should be done in a more practical environment, i.e. testing the `SearchBar` from the `App` component. These tests should ensure expected behaviour without colliding with other components.

In the case where a component needs to interact with the backend, this is currently mocked by MSW. in `client/src/test/handlers.ts`, there is a list of handlers; these assert that in testing, sending a particular http response to a specified link will return some `HttpResponse`, allowing tests to mock backends, external APIs, etc.

While frontend testing can confirm the logic of the DOM state e.g. what classes a component has, what text is displayed, it is unable to test direct visual state, e.g. responsiveness, component alignment, etc. This is more suitable to tools such as Playwright, which currently is not implemented, with no immediate plans of doing so.

### Backend
Backend testing is typically either unit tests on controller files, or integration tests on route files.

Unit tests ensure a backend function works as expected, similar to the frontend. These functions are called directly, and not via the backend route (i.e. use `testFunction()` instead of `fetch("api/testFunction")`).

Integration tests involve starting an instance of the express backend, and testing the routes (such as "api/testFunction"). External dependencies such as DBs may need to have mocked responses to function correctly. The `supertest` package allows sending HTTP responses via `request(app).get("/api/example")`, as an example, returning the response object which can be validated.

## Contact
To reach out to a team member of fn5, feel free to reach out in person (group 5), or to email at `placeholderemail@placeholder.com`
