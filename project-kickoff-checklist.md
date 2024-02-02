# Project Kickoff: General Questions

## High level questions / needs:

* Has a High Level Estimate been completed?
* What is the deadline?
* Which users will be eligible to see this and who is ineligible?
  * Consider user's membership status - Active, Cancelled, Warned, Pending, Future
  * Consider auth members, unauth, light auth, agents, etc.
  * Consider products
  * Consider billing cycles, type of billing accounts
* Will CMS be needed? Who has access?
* Are there other projects in development that could impact this one?
* If this is a new app, what onboarding is needed? What needs to be created in Jira? Need App ID?

## Data

* What are we going to measure to determine success/failure?
* What measurement tools will be needed?
* Define groups:
  * Clear definition of "Eligible", "Ineligible", "Group A", "Group B" etc. What is needed in the logs?
* Make sure project requirements and measurement plan requirements are cohesive
  * e.g. if we need data that's only available from fully authenticated members, then the project should include full auth in the requirements
* We should **always** include logs of:
  * page loads (start of flow, confirmation page if applicable)
  * form submissions
  * navigation from one app to another
  * API responses / failures

## UI

* Should we create mockups for new UI / feature?
  * Need desktop (large), tablet (medium), and mobile (small) screen sizes
* For pre-existing apps, get screenshots of existing feature / flow
  * Need desktop (large), tablet (medium), and mobile (small) screen sizes
* Use Bootstrap? [Internal UI library]? (version?)
* Are there page load processes (e.g. API calls, form submissions) needing a front-end loading spinner?
* **What will we display if any data retrieval, form submissions, etc FAIL?**
  * Inline error message?
  * Page-level error message?
  * Route to hardfall page? Use existing page or create a new one?
  * PROVIDE MOCKUPS / SCREENSHOTS

## Technical

* Confirm design, coding / Git branching standards
* What repos are needed?
  * Are there any services/repos used by the main repo we also need to onboard/understand?
  * Do we have access rights to all repos?
* Does another team need to review our project-level PR's / final release PR?
  * Who should be added as reviewers?
* **How will we get the data we need on this new app / page / feature?**
  * Will we be providing or consuming any APIs?
  * Find out proxy name(s) as well as endpoint(s) needed
  * What data is needed? (e.g. field names in API responses)
  * What auth level is needed?
  * Onboard API product(s) to app(s) if needed
  * Get links to valid OAS, and any valid postman collections

### Dev and Test Environments

* Local workspace setup:
  * What IDE? And what tools/extensions useful?
  * Any tricks to workspace or server startup
  * Test data availability and volatility
    * Consider if using the test data will then invalidate it!
* Test environment setup
  * Is there a channel to contact dependency teams for dev questions or region issues?
  * What's the deployment process?
  * Do we need to share regions? Reserve a region.

## Additional questions

* Do we have the right number of people working on this effort?
  * Avoid "too many cooks"
