This is a list of gems that are either problematic or superseded by
other gems. You should avoid using them in your projects.

* [rmagick](http://rmagick.rubyforge.org/) - this gem is notorious for its memory consumption. Use
[minimagick](https://github.com/probablycorey/mini_magick) instead.
* [autotest](http://www.zenspider.com/ZSS/Products/ZenTest/) - old solution for running tests automatically. Far
inferior to [guard](https://github.com/guard/guard) and [watchr](https://github.com/mynyml/watchr).
* [rcov](https://github.com/relevance/rcov) - code coverage tool, not
  compatible with Ruby 1.9. Use
  [SimpleCov](https://github.com/colszowka/simplecov) instead.
* [therubyracer](https://github.com/cowboyd/therubyracer) - the use of
  this gem in production is strongly discouraged as it uses a very large amount of
  memory. I'd suggest using `node.js` instead.

This list is also a work in progress. Please, let me know if you know
other popular, but flawed gems.

