One of the most important programming principles is "Don't reinvent
the wheel!". If you're faced with a certain task you should always
look around a bit for existing solutions, before rolling your
own. Here's a list of some "priceless" gems (all of them Rails 3.1
compliant) that are useful in many Rails projects:

* [active_admin](https://github.com/gregbell/active_admin) - With ActiveAdmin
  the creation of admin interface for your Rails app is child's play. You get a
  nice dashboard, CRUD UI and lots more. Very flexible and customizable.
* [better_errors](https://github.com/charliesome/better_errors) - Better Errors replaces
  the standard Rails error page with a much better and more useful error page. It is also
  usable outside of Rails in any Rack app as Rack middleware.
* [bullet](https://github.com/flyerhzm/bullet) - The Bullet gem is designed to
  help you increase your application’s performance by reducing the number of
  queries it makes. It will watch your queries while you develop your
  application and notify you when you should add eager loading (N+1 queries),
  when you’re using eager loading that isn’t necessary and when you should use
  counter cache.
* [cancan](https://github.com/ryanb/cancan) - CanCan is an authorization gem that
  lets you restrict users access to resources. All permissions are defined in a
  single file (ability.rb) and convenient methods for checking and ensuring
  permissions are available throughout the application.
* [capybara](https://github.com/jnicklas/capybara) - Capybara aims to simplify
  the process of integration testing Rack applications, such as Rails, Sinatra
  or Merb. Capybara simulates how a real user would interact with a web
  application. It is agnostic about the driver running your tests and currently
  comes with Rack::Test and Selenium support built in. HtmlUnit, WebKit and
  env.js are supported through external gems. Works great in combination with
  RSpec & Cucumber.
* [carrierwave](https://github.com/jnicklas/carrierwave) - the ultimate file
  upload solution for Rails. Support both local and cloud storage for the
  uploaded files (and many other cool things). Integrates great with
  ImageMagick for image post-processing.
* [compass-rails](https://github.com/chriseppstein/compass) - Great gem that
  adds support for some css frameworks. Includes collection of sass mixins that
  reduces code of css files and help fight with browser incompatibilities.
* [cucumber-rails](https://github.com/cucumber/cucumber-rails) - Cucumber is
  the premium tool to develop feature tests in Ruby. cucumber-rails provides
  Rails integration for Cucumber.
* [devise](https://github.com/plataformatec/devise) - Devise is full-featured
  authentication solution for Rails applications. In most cases it's preferable
  to use devise to rolling your own custom authentication solution.
* [fabrication](http://fabricationgem.org/) - a great fixture replacement
  (editor's choice).
* [factory_girl](https://github.com/thoughtbot/factory_girl) - an alternative
  to fabrication. Nice and mature fixture replacement. Spiritual ancestor of
  fabrication.
* [ffaker](https://github.com/EmmanuelOga/ffaker) - handy gem to generate dummy data
  (names, addresses, etc).
* [feedzirra](https://github.com/pauldix/feedzirra) - Very fast and flexible
  RSS/Atom feed parser.
* [friendly_id](https://github.com/norman/friendly_id) - Allows creation of
  human-readable URLs by using some descriptive attribute of the model instead
  of its id.
* [globalize](https://github.com/globalize/globalize) - Rails I18n de-facto standard
  library for ActiveRecord model/data translation. Globalize for Rails and is targeted
  at ActiveRecord version 4.x. It is compatible with and builds on the new I18n API in
  Ruby on Rails and adds model translations to ActiveRecord. For ActiveRecord 3.x users,
  check on the [3-0-stable branch](https://github.com/globalize/globalize/tree/3-0-stable).
* [guard](https://github.com/guard/guard) - fantastic gem that monitors file
  changes and invokes tasks based on them. Loaded with lots of useful
  extension. Far superior to autotest and watchr.
* [haml-rails](https://github.com/indirect/haml-rails) - haml-rails provides
  Rails integration for Haml.
* [haml](http://haml-lang.com) - HAML is a concise templating language,
  considered by many (including yours truly) to be far superior to Erb.
* [kaminari](https://github.com/amatsuda/kaminari) - Great paginating solution.
* [machinist](https://github.com/notahat/machinist) - Fixtures aren't fun.
  Machinist is.
* [rspec-rails](https://github.com/rspec/rspec-rails) - RSpec is a replacement
  for Test::MiniTest. I cannot recommend highly enough RSpec. rspec-rails
  provides Rails integration for RSpec.
* [sidekiq](https://github.com/mperham/sidekiq) - Sidekiq is probably
  the easiest and most scalable way to run background jobs in your
  Rails app.
* [simple_form](https://github.com/plataformatec/simple_form) - once you've
  used simple_form (or formtastic) you'll never want to hear about Rails's
  default forms. It has a great DSL for building forms and no opinion on
  markup.
* [simplecov-rcov](https://github.com/fguillen/simplecov-rcov) - RCov formatter
  for SimpleCov. Useful if you're trying to use SimpleCov with the Hudson
  contininous integration server.
* [simplecov](https://github.com/colszowka/simplecov) - code coverage tool.
  Unlike RCov it's fully compatible with Ruby 1.9. Generates great reports.
  Must have!
* [slim](http://slim-lang.com) - Slim is a concise templating language,
  considered by many far superior to HAML (not to mention Erb). The only thing
  stopping me from using Slim massively is the lack of good support in major
  editors/IDEs. Its performance is phenomenal.
* [spork](https://github.com/sporkrb/spork) - A DRb server for testing
  frameworks (RSpec / Cucumber currently) that forks before each run to ensure
  a clean testing state. Simply put it preloads a lot of test environment and
  as consequence the startup time of your tests in greatly decreased. Absolute
  must have!
* [sunspot](https://github.com/sunspot/sunspot) - SOLR powered full-text search
  engine.

This list is not exhaustive and other gems might be added to it along
the road. All of the gems on the list are field tested, have active
development and community and are known to be of good code quality.

