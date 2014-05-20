* Use `%()`(it's a shorthand for `%Q`) for single-line strings which require both
  interpolation and embedded double-quotes. For multi-line strings, prefer heredocs.

  ```Ruby
  # bad (no interpolation needed)
  %(<div class="text">Some text</div>)
  # should be '<div class="text">Some text</div>'

  # bad (no double-quotes)
  %(This is #{quality} style)
  # should be "This is #{quality} style"

  # bad (multiple lines)
  %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
  # should be a heredoc.

  # good (requires interpolation, has quotes, single line)
  %(<tr><td class="name">#{name}</td>)
  ```

* Avoid `%q` unless you have a string with both `'` and `"` in
  it. Regular string literals are more readable and should be
  preferred unless a lot of characters would have to be escaped in
  them.

  ```Ruby
  # bad
  name = %q(Bruce Wayne)
  time = %q(8 o'clock)
  question = %q("What did you say?")

  # good
  name = 'Bruce Wayne'
  time = "8 o'clock"
  question = '"What did you say?"'
  ```

* Use `%r` only for regular expressions matching *more than* one '/' character.

  ```Ruby
  # bad
  %r(\s+)

  # still bad
  %r(^/(.*)$)
  # should be /^\/(.*)$/

  # good
  %r(^/blog/2011/(.*)$)
  ```

* Avoid the use of `%x` unless you're going to invoke a command with backquotes in
  it(which is rather unlikely).

  ```Ruby
  # bad
  date = %x(date)

  # good
  date = `date`
  echo = %x(echo `date`)
  ```

* Avoid the use of `%s`. It seems that the community has decided
  `:"some string"` is the preferred way to create a symbol with
  spaces in it.

* Prefer `()` as delimiters for all `%` literals, except `%r`. Since
  braces often appear inside regular expressions in many scenarios a
  less common character like `{` might be a better choice for a
  delimiter, depending on the regexp's content.

  ```Ruby
  # bad
  %w[one two three]
  %q{"Test's king!", John said.}

  # good
  %w(one two three)
  %q("Test's king!", John said.)
  ```

