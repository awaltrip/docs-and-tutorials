# Pull request template

Below is a standard template for developer Pull Requests.

Remove checklist items that will be irrelevant to your app (e.g., back-end apps/services may not need accessibility or browser testing).

Update checklist items as needed.

[How to create an auto generated Pull Request template for your repository](https://docs.github.com/en/free-pro-team@latest/github/building-a-strong-community/creating-a-pull-request-template-for-your-repository)

***

## Changes

_Replace this text with a summary / list of the changes you're making in this PR. Make it simple for your teammates to understand._

* Change 1
* Change 2, etc

## Checklist

**Before opening a PR, check that you have completed all the following:**

* [ ] Incremented the app version number appropriately, or N/A.
      <details>
        <summary>
          <i>How to increment version numbers</i>
        </summary>
        <ul>
          <li>New features should increment the middle (MINOR) version number (e.g. 0.1.0).</li>
          <li>Bug fixes or small changes that don't add a new feature should increment the last (PATCH) version number (e.g. 0.0.1).</li>
        </ul>
      </details>
* [ ] Manually tested my changes in { a browser | postman | etc }, or N/A.
* [ ] Manually tested my changes for responsiveness (mobile, tablet, changing screen size), or N/A.
* [ ] Added unit tests for all my code changes, or N/A.
  * Tests should not throw `spec '...' has no expectations` warnings except in rare cases.
* [ ] Updated the Postman collection if I added a request or changed any request requirements, or N/A.
      <details>
        <summary>
          <i>How to update the Postman collection</i>
        </summary>
        <ul>
          <li>In your list of Collections in Postman, hover over the collection name and click on the 3 dots.</li>
          <li>Click Export -> Collection v2.1.</li>
          <li>Save the exported collection to the docs folder in this repo (replace the file that's already there).</li>
        </ul>
      </details>
* [ ] Removed any commented out code, console logs, focused tests, etc.
* [ ] Ran aXe extension in the browser, or N/A.
* [ ] Checked my changes against our { accessibility standards (link) }, or N/A.
* [ ] Ran CI check locally and made sure it passed. CI check includes:
  * Install
  * Build
  * Linting
  * Unit Tests
* [ ] Reviewed my own changes by comparing branches on GitHub.
  * PR does not include accidental code changes, accidental formatting changes, etc.
* [ ] Made sure my PR name takes an approved format. Examples:
  * [examples]
