## Git Branch Naming

Use a uniform syntax when naming branches. When multiple projects are involved in a feature implementation, use matching names.

```
<ticket-id>/<feature-name>
```

**Ticket ID**

A reference to the Jira or Clubhouse ticket associated with the task. This makes it possible for the Github integration in Jira or Clubhouse to link to the branch from the ticket.

New Jira tickets ids must start with ```PD``` for 'Product Development' for example ```PD-4```

**Feature Name**

A short description of the feature, formatted in `kebab-case`, that makes it easy to identify when switching between branches.

**Sample Branch Checkout:**

```
git checkout -b PD-43/analytics-user-bug upstream/master
```

## Git Commit Format

A git commit message can be a valuable tool when debugging issues. Commits are a natural place for developers to provide clues and context for the changes they are making. Make writing meaningful commit messages a part of your standard workflow. Putting in the extra work up front may just pay dividends to the team or even your future self.

> This format is inspired by Google's git conventions for the Angular project. For a detailed explanation of Google's guidelines and conventions, see [this document](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit)

### Commit Message Format

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

**Type**

Must be one of the following:

* **feat**: A new feature
* **fix**: A bug fix
* **docs**: Documentation only changes
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **perf**: A code change that improves performance
* **test**: Adding missing tests
* **chore**: Changes to the build process or auxiliary tools and libraries such as documentation generation
* **fuck**: A fix that addresses catastrophic failure or gross negligence

**Scope**

The scope could be anything specifying the place of the commit change, such as a feature module or component. Should be written in `camelCase`

**Subject**

The subject contains succinct description of the change:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize first letter
* no dot (.) at the end

**Body**

Just as in the subject, use the imperative, present tense: "change" not "changed" nor "changes" The body should include the motivation for the change and contrast this with previous behavior.

**Footer**

The footer should contain any information about Breaking Changes and is also the place to reference Jira or Clubhouse issues that this commit Closes.

Breaking Changes are intended to highlight (in the ChangeLog) changes that will require community users to modify their code with this commit.

**Sample Commit:**

```
fix(eventTracker): analytics.user not a function bug

Replace `$window.analytics` with `window.analytics` because analytics isn't set on the window until after the async library is loaded.

See: https://github.com/segmentio/analytics.js/issues/527

Closes [ch332]
```

## Automated Tests

Prior to opening a PR you must write the best suite of automated tests possible given the current state of the automated testing platform available to developers at Portfolium. As the state of the automated testing platform is updated changes will be recorded here.

For all UI components, developers are required to create a Mabl test to verify the core functionality of the feature can be executed through the test. All data required for the test should be staged on the QA database. If the test requires the manipulation of data, the test should restore the data to the original state after asserting the feature in question. Tests should be grouped by Platform and then by Feature. Naming conventions for platforms and features TBD. (Estimated 10/31/2018)

NOTE: All Mabl test flows should be approximately 6 steps to increase code reuse. Most Mabl tests will include a few small flows (login, navigate to page X, etc.) and then a new flow to verify the feature created. Expect your flows to be reused by other tests in the environment.

For all API endpoints, developers should write an appropriate POSTMAN test to verify the endpoint performs as expected. Remember, pre and post scripts can be attached to endpoints to stage and destory data to avoid polluting the database. 

Example:
To test submitting a course assignment, stage the data on QA such that you can login as the user and be already enrolled in the course. Navigate to the course assignment page. Submit the course assignment. Assert the page has changed to the submitted assignment state. Then revert the data to the original state by Unsubmitting the assignment. 

While this solution is not perfect it will serve as a starting point for our automated testing platform. 

Remember, data on the QA database must be treated as sacrosanct for these tests and can not be modified. If you modify data and disrupts a test you will be laughed at. 

During the Code Review process of the pull request the automated tests will be reviewed to determine if they meet these guidlines and appropriately test the feature you have created. 

## Opening your PR

When you are ready to have your work peer reviewed before requesting QA (and eventually going to master), you'll open a PR from your branch into the development branch of the project you are working on.

Before doing so, you should:
* Rebase with development
* Rebase your own branch to remove uneeded and extranous commit messages

Once you recieve a request during your code review to update or fix code you then:
* Follow the same conventions as normal commits -- no "clean up" or "oops" messages -- because these commits won't be rebased and will appear in history on master
* Continue to merge with development daily

## Move and update your Jira or Clubhouse ticket

Once your PR has been opened, you should move your ticket to the correct swim lane, most likely Code Review. However if your code has passed Code Review and it's ready for PM/QA you should then move the ticket again.

After moving your ticket, you should be ready to let the PM know they can check it for acceptance. Here is a sample comment you can add to your ticket:

```
@mark my work is ready for PM acceptance, it will be staged on DEV3

The branches that need to be deployed for this features are:
WEB: <BRANCH NAME>
API: <BRANCH NAME> and DOES/DOES NOT require a migration
EDU: <BRANCH NAME>
ADMIN: <BRANCH NAME>
```


