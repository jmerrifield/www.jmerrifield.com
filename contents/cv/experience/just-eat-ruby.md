---
company: Just-Eat
position: Developer - Test Automation (Ruby)
start: 2010-12-01
end: 2013-01-01
tags:
  - cucumber
  - capybara
  - activerecord
  - ruby
  - teamcity
location: Farringdon, London
---

Implemented an automated test framework for the system in Cucumber, using Capybara for web interaction and ActiveRecord to inject setup data and make assertions against data. Created a set of emulators to mimic the external systems that get called during functional tests (e.g. payment gateways, GSM terminals).

Configured TeamCity to run the tests automatically, so that whenever a commit is made to source control, the code is compiled, deployed to 8 staging environments (one for each country we support), and then the tests are run (currently around 200 scenarios, covering country-specific nuances, and the mobile UI through user-agent spoofing in selenium/webdriver).

Built a custom Cucumber harness, which invokes Cucumber once for each environment, aggregates the results, re-runs any failed tests (to reduce the number of false-negatives arising due to transient issues e.g. timeouts), and then creates a custom HTML report showing the status of each environment. Also built a custom TeamCity formatter for Cucumber so that it can deal with the multiple environments, and multiple runs of failed tests.

In addition to building the framework, I also support the QA engineers and developers who use it within their teams. This is both technical in nature - helping out with Ruby syntax, diagnosing tests that are failing falsely (or indeed, passing falsely) - and high level - for example holding regular workshops where interested team members come to discuss the best approach to testing a particular aspect of the system. These discussions usually center around how to express system behaviour in Gherkin in a way that is both readable, and concrete enough to build step definitions around.