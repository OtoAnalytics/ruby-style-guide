* Write `ruby -w` safe code.

* Avoid hashes as optional parameters. Does the method do too much? (Object initializers are exceptions for this rule).

* Avoid methods longer than 10 LOC (lines of code). Ideally, most methods will be shorter than
  5 LOC. Empty lines do not contribute to the relevant LOC.

* Avoid parameter lists longer than three or four parameters.

* If you really need "global" methods, add them to Kernel
  and make them private.

* Use module instance variables instead of global variables.

  ```Ruby
  # bad
  $foo_bar = 1

  # good
  module Foo
    class << self
      attr_accessor :bar
    end
  end

  Foo.bar = 1
  ```

* Avoid `alias` when `alias_method` will do.

* Use `OptionParser` for parsing complex command line options and
`ruby -s` for trivial command line options.

* Prefer `Time.now` over `Time.new` when retrieving the current system time.

* Code in a functional way, avoiding mutation when that makes sense.

* Do not mutate arguments unless that is the purpose of the method.

* Avoid more than three levels of block nesting.

* Be consistent. In an ideal world, be consistent with these guidelines.

* Use common sense.

