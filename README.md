How We Work
===========

## Values & Core Principles

* Fairness
* Joy
* [Kaizen](https://en.wikipedia.org/wiki/Kaizen)

## Other Guides:

* [For Product Owners](product.md)

## Formatting/Conventions

Base styles guides:

* Ruby - [bbatsov/ruby-style-guide](https://github.com/bbatsov/ruby-style-guide)
* CSS - [JT CSS Style Guide](https://github.com/jetthoughts/how-we-work/blob/master/css.md)
* JavaScript - [airbnb/javascript](https://github.com/airbnb/javascript)

Our updates:

* Limit lines to 110 characters, in order to remove horizontal scrolling on GitHub when we are doing code review
* Align parameters like:

```ruby
# good (normal indent) PREFERABLE
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com',
    from: 'us@example.com',
    subject: 'Important message',
    body: source.text
  )
end

# not so bad
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com', from: 'us@example.com'
  )
end

# good, but DEPRECATED
def send_mail(source)
  Mailer.deliver(to: 'bob@example.com',
                 from: 'us@example.com',
                 subject: 'Important message',
                 body: source.text)
end
```
* Use prefix `_` for memo variables:
 
```ruby
class TestObject
  attr_reader :attr_name
  
  def attr_name
    @attr_name ||= lazy_calculation_for_attr_name
  end
  
  def public_method_with_memo
    @_public_method_with_memo ||= public_method_with_memo_calculcations
  end
end
```

* Stick to [Newlines](https://github.com/airbnb/ruby#newlines) section of Airbnb's Ruby style guide for grouping the code within methods.

## Working with Bugs

* All bugs should be covered with tests and by TDD

## Ruby on Rails Conventions

* We use Decorators (in code we called them `Carrier`) as View and Form objects: [introduction how to use them](https://goo.gl/photos/nN1yNNqUoyKEK6an7)
* We do not use full Presenters (TODO: add link to first post about them) with tag generations
* We do not over use by [Concerns](https://blog.codeship.com/when-to-be-concerned-about-concerns/)

## Setup Development Environment

* `bin/setup` - cold setup
* `rake setup`
* `rake setup_sample_data`

## Delivery Flow

* create PR
* deploy PR to Heroku
* ask verify, to code review and to merge

## TODO/FIXME Notes

* add issue on GitHub per each note
* create TODO/FIXME note in the code
* add in code's note link to GitHub's issue

## General templates

* JavaScript Page logic organisation: https://github.com/tastejs/todomvc/blob/gh-pages/examples/jquery/js/app.js
 
## Git/GitHub

* Prefix feature branch names with issue number: 123-issue-name;
* do not mess with cosmetics changes;
* Squash multiple trivial commits into a single commit;
* Convert an existing issue into a pull request: `hub pull-request -i 123`;
* Write a good commit message based on http://chris.beams.io/posts/git-commit/ with some requirements:
  ```
  #<github_id>: Capitalized, short (50 chars or less) summary
  
  More detailed explanatory ...
  
  Closes #<other_github_issue_id>
  ```
  Also some examples:

  * http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  * https://robots.thoughtbot.com/5-useful-tips-for-a-better-commit-message
  
* Project management:
  * Used user stories format: https://www.mountaingoatsoftware.com/agile/user-stories and http://www.alexandercowan.com/best-agile-user-story/
  * Tests scenarios and Reproduction steps format: https://github.com/cucumber/cucumber/wiki/Given-When-Then

* Tutorials:
  * https://www.atlassian.com/git/tutorials/
  * http://git-scm.com/docs/gittutorial
  * https://try.github.io/ 

## Development Best Practices

* [Exceptions should be exceptional.](http://etdev.me/pragmatic/34/)
* [KISS ... your ARSE :P](http://code.mumak.net/2012/02/simple-made-easy.html)
* Stub/Mock only external services or code with hard simulation: https://www.youtube.com/watch?v=z9quxZsLcfo&feature=youtu.be&t=21m00s
* [Four-Phase Test](http://xunitpatterns.com/Four%20Phase%20Test.html)

## Other Tools and Practices to use

* [UX from Good UI](http://www.goodui.org/)
* [Material design](https://material.io/)

## Tutorials
* HTML/CSS3:
  * [Learn CSS Layout](http://learnlayout.com/)
* Web Performance:
  * [Website Performance Optimization: The Critical Rendering Path](https://www.udacity.com/course/ud884)
* ES6: https://www.eventbrite.com/engineering/tag/learning-es6/
  

## Constraints which makes fun development

* 2 days per PR
* 2 Issues/PR per Developer
* [1000/100/6 performance model](https://www.paulirish.com/2015/advanced-performance-audits-with-devtools/)
* 5 min to pass all test suites
* 20 sec to run one test
* 20 sec to boot

## Tools:
* Collaboration:
  * Chat: Slack
  * Issues Plannings: Github, Trello and Waffle.io
  * Information board: Hackpad, Google Site, Trello
  * Screenshots: Skitch (OS X), Screencloud (Ubuntu, OS X)
  * Screencast: Kazam (Ubuntu)
* CI:
  * TeamCity (self hosted)
  * CircleCI
* Server Conf: Chef
* Deployments: Capistrano
* Assets and File Uploads CDN hosting: AWS, Cloudinary (Images Uploads)
* PAAS for Isolated Staging Testing: Heroku (Rails apps), divshot.io (static HTML)
* Cache: Memcached Cloud from Redis Lab
* JavaScript Base Frameworks: jQuery, React.js, Angular.js, Backbone.js
* SCM: Git on GitHub
