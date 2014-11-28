How We Work
===========


## Formatting

As usual we use [bbatsov/ruby-style-guide](https://github.com/bbatsov/ruby-style-guide), 
but have some specific usage:

* Limit lines to 110 characters, in order to remove horizontal scrolling on GitHub when we are doing code review
* Align parameters like:

```ruby
# not so bad
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com', from: 'us@example.com'
  )
end

# good
def send_mail(source)
  Mailer.deliver(to: 'bob@example.com',
                 from: 'us@example.com',
                 subject: 'Important message',
                 body: source.text)
end

# good (normal indent)
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com',
    from: 'us@example.com',
    subject: 'Important message',
    body: source.text
  )
end
```

## Working with Bugs

* All bugs should be covered with tests and by TDD

## Simplify Views

* We use Decorators (in code we called them `Carrier`) as View and Form objects
* We do not use full Presenters (TODO: add link to first post about them) with tag generations

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
 
## Git/GitHub

* Prefix feature branch names with issue number.
* do not mess with cosmetics changes
* Squash multiple trivial commits into a single commit.
* Write a good commit message based on http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html with some requirements:
  ```
  #<github_id>: Capitalized, short (50 chars or less) summary
  
  More detailed explanatory ...
  
  Closes #<other_github_issue_id>
  ```
   

## Best Practices

* [Exceptions should be exceptional.](http://pragmatictips.com/34)
* [KISS ... your ARSE :P](http://code.mumak.net/2012/02/simple-made-easy.html)

## Tutorials
* HTML/CSS3:
  * [Learn CSS Layout](http://learnlayout.com/)
* Web Performance:
  * [Website Performance Optimization: The Critical Rendering Path](https://www.udacity.com/course/ud884)

