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


