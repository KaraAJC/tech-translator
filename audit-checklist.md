---
description: The full audit checklist
---

# Audit Checklist

### Security

* How are the credentials being stored?
* Who has access to credentials in the organization?
* How are credentials saved into source code?
* Do any 3rd Party Integrations contain weak passwords?
* Are they using proper credential hygiene?

### Infrastructure

* What are the Application Server Specs?
* What is the load balancer setup?
* Is there orchestration setup, eg Chef, Ansible, Etc.?
* What are the system dependencies eg ImageMagick?
* What is actually running on the server, vs what should be?
* How is email being sent?
* Is there any sort of caching?
* Are there any scheduled tasks?
* Are there any Custom rake tasks?
* Is there an SSL Certificate?
  * When does it expire?
  * Is the SSL Certificate being enforced for the login/payment flows?
* Are assets served successfully and properly over HTTPS?

### Database

* What are the Database Server specs?
* What version of DB is being used?
* What are the table sizes \(in GB, and in Rows\)
* What are the table storage engines being used?
* What is the current replication strategy?
* are there regular backups being made?
* What is the status of the Data's integrity and performance?
  * Do indexes exist?
  * Do Foreign Keys exist?
* What is the chosen DB engine vs Optimal DB Engine _(e.g. Mongo vs Postgres?)_

### Third-party Services

* What Services are being used?
  * Get access to each service.

_Examples:_
  * Marketing email, _e.g. Campaign Monitor, Mailchimp, etc._
  * Application emails, _e.g. Sendgrid, Mailgun, etc._
  * Performance monitoring, _e.g. New Relic, Skylight, etc._
  * Uptime monitoring, _e.g. Pingdom_
  * Analytics, _e.g. Google Analytics, Mixpanel, etc._
  * Exception-Notification system, _e.g. Rollbar, or ExceptionNotifier_
  * Android App Keychain
  * Facebook Login application
  * Google Webmaster Tools

### Rails

* Assets
  * Are they being minified in production?
  * Are they being served properly with gzip?

* Gemfile
  * number?
  * anything unfamiliar?
  * how out of date?
    Check `bundle outdated`. Use bundler-audit too.

* Tests
  * What is the Code Coverage percent
  * What kinds of tests are there?
  * What is the quality of the tests?
  * What is the Code Quality Grade?

* Async/queuing
  * Is Devise set up to perform async e-mailing?

* Webhook endpoints
  * from which services? are they documented in the README?
  * Are there actions from the webhooks which should be background tasks to improve response time to the webhook?
  * What endpoints/classes do the JavaScript functions depend on?
* Are JavaScript functions bound against ID or Class names (should be “js--prefix” classes)
* Are there vendored assets?
  * Are the minimum number of vendored assets included in the asset pipeline (to minimize the filesize)
* Are there any javascript errors when going through all the possible pages of the app
* Are there any hard-coded object-ids in the codebase (e.g. if user.id == 19 then….)
* Are views doing correct Eager Loading of data to improve performance?
* Are there places where we are loading too much data at once, and should perform `find_each` with reduced batch_size to improve memory footprint?
* Are we storing money as float? (should use Money gem instead)

### Rails UI
* What Front-end dependencies are there?
* What Browser/Versions are they purported to support?
  * Should we do a cross-browser test to double-check?
* Is the HTML structure well designed?
* Is the CSS written in a way that makes it easy to move elements around?
  **Consider bringing a UI developer in to evaluate this part**

### Developer Support

* Is there a CI setup?
* Is there a thorough README describing how to successfully set up a development environment
* Does the README include instructions on all of the 3rd party integrations, and settings for each
* Does the README describe scheduled tasks
* Is there a tool for being informed of exceptions? (ExceptionNotification/Rollbar/AirBrake)
* Is there a tool for monitoring request performance? (NewRelic/Skylight)
* Does the Staging server have a MailerInterceptor installed?
* Are there boolean fields which can be nil?

### Static Analysis

- Use code climate to get a GPA and identify areas of complexity, duplication, etc.
- Use brakeman to do a test for security vulnerabilities.

### iOS

* Dependency management system
* Deployment target version
* Deprecation warnings
* Duplicated code
* View controller size
* Environment setup
* Build management
* Storyboards or not

### API

* Does the application support any API clients?
  * What are the JSON/XML responses to actions

### Visual Assets

* Do we have raw assets? (images, icons, etc)

### Access

* Do they have a solid Authentication/Authorization pattern? (authorizing each action?)

### Quality Audit

* Does the code show proper separation of concerns, thin controllers, validation at the proper points?
* Is there a minimal amount of conditional logic in the views?

### Configuration Management and Security

### Infrastructure migration

* Are there areas of tech which we aren't familiar with? (parse.io, mongodb, etc)

### Deployment

* Are logs being rotated
* Is the infrastructure upgraded to deal with any known security vulnerabilities?

### Business/Operations

* Who is the Product owner who can make decisions in changes to the application's behavior?
* Is the IOS App Store EIN changing? (new business owner means new iOS app)
* Do we have access to the existing feedback mechanisms? (email, user forums, etc)
