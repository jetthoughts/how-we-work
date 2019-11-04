JTology - How We Work
===========

## Values & Core Principles

* Fairness
* Joy
* [Kaizen](https://en.wikipedia.org/wiki/Kaizen)

## Other Guides:

* [For Product Owners](product.md)
* [Thoughtbot's Guides](https://github.com/thoughtbot/guides)

## Base Strucutring Projects

* SCSS: Structure is based on [RSCSS](https://github.com/rstacruz/rscss)
* Vanila JavaScript: Strucutre is based on [RSJS](https://github.com/rstacruz/rsjs)
* Other common structure of JavaScript Page logic: https://github.com/tastejs/todomvc/blob/gh-pages/examples/jquery/js/app.js

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

* All bugs should be covered with tests and by **TDD**

## Ruby on Rails Conventions

* We use Decorators (in code we called them `Carrier`) as View and Form objects: [introduction how to use them](https://goo.gl/photos/nN1yNNqUoyKEK6an7)
* We do not use full Presenters (TODO: add link to first post about them) with any tag generations
* We do not overuse of [Concerns](https://blog.codeship.com/when-to-be-concerned-about-concerns/)
* <a name="prevent-syntax-sugar-overuse"></a>We do not overuse (in 99% of our code we do not see such stuff): `send`, `&.`, `**`. To prevent misusage of Ruby Syntax Sugars <sup>[[link](#prevent-syntax-sugar-overuse)]</sup>

## Test Conventions

* <a name="meaningful-names-in-tests"></a>We use the meaningful names in the test cases. It makes easier to understand the business logic.<sup>[[link](#meaningful-names-in-tests)]</sup>

```ruby
# bad
def test_email_is_normalized
  user = User.create! email: 'Foo@quux.com'
  assert_equal 'foo@quux.com', user.email
end

# good
def test_email_is_normalized
  user = User.create! email: ' thisIsAMixedCaseEmail@example.com'
  assert_equal 'thisisamixedcaseemail@example.com', user.email
end
```
* <a name="big-fixtures-in-tests">Do not load more data than needed to test your code. For each test create exactly what it needs and not more. More variations provides more complexities.<sup>[[link](#big-fixtures-in-tests)]</sup>

```ruby
# BAD
let!(:user_with_big_name) { ... }
let!(:user_with_small_name) { ... }

it 'this test use only user_with_big_name' { expects(response).to have(user_with_big_name) }
it 'this test use only user_with_small_name' { expects(response).to have(user_with_small_name) }
```

```ruby
# GOOD
context 'with big name' do
  let(:user) { ... }
  
  it 'this test use only user_with_big_name' { expects(response).to have(user) }
end

context 'with small name' do
  let(:user) { ... }
  
  it 'this test use only user_with_small_name' { expects(response).to have(user) }
end
```

```ruby
# BAD
setup do
  big_file_with_all_users = compile_file_from_users(User.all)
end

test 'this test use only user_with_big_name' { assert_includes big_file_with_all_users, 'magic string with all big letter' }
test 'this test use only user_with_small_name' { assert_includes big_file_with_all_users, 'magic string with all small letter' }
```

```ruby
# GOOD
test 'this test use only user_with_big_name' do
  result = compile_file_from_users(User.new(name: 'Big Name'))
  assert_includes result, 'Big Name'
end

test 'this test use only user_with_small_name' do
  result = compile_file_from_users(User.new(name: 'Samll Name'))
  assert_includes result, 'Small Name'
end
```

* <a name="dynamic-cases-in-tests">No Dynamic Test generation.<sup>[[link](#dynamic-cases-in-tests)]</sup>

```ruby
# BAD
{ string: 'zone_id', array: %w[zone_id], hash: { "0" => "zone_id" } }.each do |type, group_by|
  it "returns valid json if group_by is #{type}" do
  end
end
```

```ruby
# GOOD
it "returns zone_id json if group_by is string" { }
it "returns [zone_id] json if group_by is array" { }
it "returns { '0' => 'zone_id' } json if group_by is hash" { }
```

## Setup Development Environment

* `bin/setup` - cold setup
* `bin/update` - update environment on new code updates

## Delivery Flow

Our flow is based on GitHub flow with Heroku Review

* create PR (we convert issues into PR)
* deploy PR to Heroku (we use Heroku Review to do this automatically)
* verify on Heroku yourselves
* ask verify, to code review and to merge (we have Code Review)

## TODO/FIXME Notes

* add issue on GitHub per each note
* create TODO/FIXME note in the code
* add in code's note link to GitHub's issue
 
## Git/GitHub

* [Basic git crash course for minimum git commands enough to work on the project](https://jtway.co/how-do-we-git-it-in-jetthoughts-a002b4dba223)
* Prefix feature branch names with issue number: *123-issue-name*;
* Do not mess with cosmetics changes. Move them in separate commit or pr;
* Squash multiple trivial commits into a single commit;
* Convert an existing issue into a pull request: `hub pull-request -i 123`;
* <a name="git-commit-message"></a>Write a good commit message based on http://chris.beams.io/posts/git-commit/ with some requirements<sup>[[link](#git-commit-message)]</sup>:
  ```
  Capitalized, the imperative mood, short (50 chars or less) subject (#<github_id>)
  
  Body after space line. Wrap the body at 72 characters.
  Use the body to explain what and why.
  
  Closes #<other_github_issue_id>, fixes #<another_github_issue_id>
  ```
  Also some examples:

  * http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  * https://robots.thoughtbot.com/5-useful-tips-for-a-better-commit-message
  * https://github.com/RomuloOliveira/commit-messages-guide
  
* <a name="git-issue-template"></a> Create Issue Template<sup>[[link](#git-issue-template)]</sup>
    * **Title:** Jobs to be done
    * **Body:**
    
      *1. Acceptance Criteria*
      
      Acceptance criteria is that a developer knows they need to complete before that issue can be considered 'done'.
      They are the points against which the issue will be tested.

      *2. A screenshot or mock up of a new design*
   
       A picture which illustrates what the issue should be creating or a screenshot of an existing page showing where a bug is occurring.
       Remember to include mock ups of both mobile and desktop views.

* Tutorials:
  * https://www.atlassian.com/git/tutorials/
  * http://git-scm.com/docs/gittutorial
  * https://try.github.io/ 

## Development Best Practices

* [Exceptions should be exceptional](https://jacopretorius.net/2009/10/exceptions-should-be-exceptional.html)
* [KISS ... your ARSE :P](http://code.mumak.net/2012/02/simple-made-easy.html)
* Stub/Mock only external services or code with hard simulation: https://www.youtube.com/watch?v=z9quxZsLcfo&feature=youtu.be&t=21m00s
* [Four-Phase Test](http://xunitpatterns.com/Four%20Phase%20Test.html)

## Other Tools and Practices to use

* [UX from Good UI](http://www.goodui.org/)
* [Material design](https://material.io/)

## Recomended Tutorials

* HTML/CSS3:
  * [Learn CSS Layout](http://learnlayout.com/)
  * [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* Web Performance:
  * [Website Performance Optimization: The Critical Rendering Path](https://www.udacity.com/course/ud884)
* ES6: https://www.eventbrite.com/engineering/tag/learning-es6/
* React.js/Redux: https://egghead.io/browse/frameworks/react
  

## Constraints which makes fun development

* 2 days per PR
* 2 Issues/PR per Developer
* [1000/100/6 performance model](https://www.paulirish.com/2015/advanced-performance-audits-with-devtools/)
* 5 min to pass all test suites
* 20 sec to run one test
* 20 sec to boot

## Tools:
* Collaboration:
  * Chat: [Discord](https://discordapp.com/)
  * Issues Plannings: [Github](https://github.com), [Trello](https://trello.com)
  * Information board: [Trello](https://trello.com)
  * Screenshots: [CloudApp](https://www.getcloudapp.com/), [Joxi](http://joxi.net/) (Ubuntu)
  * Screencast: [Loom](https://www.useloom.com), Kazam (Ubuntu)
  * Video call: [Appear.in](https://appear.in/)
* CI:
  * [CircleCI](https://circleci.com/)
* Server Configuation: [Ansible](https://www.ansible.com/)
* Deployments: Capistrano
* Assets and File Uploads CDN hosting: AWS, CloudFront, Cloudinary (Images Uploads)
* PAAS for Isolated Staging Testing: [Heroku](https://heroku.com) (Ruby on Rails apps), [surge.sh](http://surge.sh/) (Static HTML)
* Cache: Memcached/Redis Cloud from Redis Lab
* JavaScript Base Frameworks: [Stimulus](https://github.com/stimulusjs/stimulus), Vanilla JS, [Vue.js](https://vuejs.org/), [React](https://reactjs.org/)
* SCM: [GitHub](https://github.com)
