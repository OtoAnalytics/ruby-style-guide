> Some people, when confronted with a problem, think
> "I know, I'll use regular expressions." Now they have two problems.<br/>
> -- Jamie Zawinski

* Don't use regular expressions if you just need plain text search in string:
  `string['text']`

* For simple constructions you can use regexp directly through string index.

  ```Ruby
  match = string[/regexp/]             # get content of matched regexp
  first_group = string[/text(grp)/, 1] # get content of captured group
  string[/text (grp)/, 1] = 'replace'  # string => 'text replace'
  ```

* Use non-capturing groups when you don't use captured result of parentheses.

  ```Ruby
  /(first|second)/   # bad
  /(?:first|second)/ # good
  ```

* Don't use the cryptic Perl-legacy variables denoting last regexp group matches
  (`$1`, `$2`, etc). Use `Regexp.last_match[n]` instead.

  ```Ruby
  /(regexp)/ =~ string
  ...

  # bad
  process $1

  # good
  process Regexp.last_match[1]
  ```

* Avoid using numbered groups as it can be hard to track what they contain. Named groups
  can be used instead.

  ```Ruby
  # bad
  /(regexp)/ =~ string
  ...
  process Regexp.last_match[1]

  # good
  /(?<meaningful_var>regexp)/ =~ string
  ...
  process meaningful_var
  ```

* Character classes have only a few special characters you should care about:
  `^`, `-`, `\`, `]`, so don't escape `.` or brackets in `[]`.

* Be careful with `^` and `$` as they match start/end of line, not string endings.
  If you want to match the whole string use: `\A` and `\z` (not to be
  confused with `\Z` which is the equivalent of `/\n?\z/`).

  ```Ruby
  string = "some injection\nusername"
  string[/^username$/]   # matches
  string[/\Ausername\z/] # doesn't match
  ```

* Use `x` modifier for complex regexps. This makes them more readable and you
  can add some useful comments. Just be careful as spaces are ignored.

  ```Ruby
  regexp = /
    start         # some text
    \s            # white space char
    (group)       # first group
    (?:alt1|alt2) # some alternation
    end
  /x
  ```

* For complex replacements `sub`/`gsub` can be used with block or hash.

