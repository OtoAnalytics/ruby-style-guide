> The only real difficulties in programming are cache invalidation and
> naming things. <br/>
> -- Phil Karlton

* Name identifiers in English.

  ```Ruby
  # bad - identifier using non-ascii characters
  заплата = 1_000

  # bad - identifier is a Bulgarian word, written with Latin
letters (instead of Cyrillic)
  zaplata = 1_000

  # good
  salary = 1_000
  ```

* Use `snake_case` for symbols, methods and variables.

  ```Ruby
  # bad
  :'some symbol'
  :SomeSymbol
  :someSymbol

  someVar = 5

  def someMethod
    ...
  end

  def SomeMethod
   ...
  end

  # good
  :some_symbol

  def some_method
    ...
  end
  ```

* Use `CamelCase` for classes and modules.  (Keep acronyms like HTTP,
  RFC, XML uppercase.)

  ```Ruby
  # bad
  class Someclass
    ...
  end

  class Some_Class
    ...
  end

  class SomeXml
    ...
  end

  # good
  class SomeClass
    ...
  end

  class SomeXML
    ...
  end
  ```

* Use `snake_case` for naming files, e.g. `hello_world.rb`.

* Use `snake_case` for naming directories, e.g.
  `lib/hello_world/hello_world.rb`.

* Aim to have just a single class/module per source file. Name the
  file name as
  the class/module, but replacing CamelCase with snake_case.

* Use `SCREAMING_SNAKE_CASE` for other constants.

  ```Ruby
  # bad
  SomeConst = 5

  # good
  SOME_CONST = 5
  ```

* The names of predicate methods (methods that return a boolean value)
  should end in a question mark.
  (i.e. `Array#empty?`). Methods that don't return a boolean, shouldn't
  end in a question mark.

* The names of potentially *dangerous* methods (i.e. methods that
  modify `self` or the arguments, `exit!` (doesn't run the finalizers
  like `exit` does), etc.) should end with an exclamation mark if
  there exists a safe version of that *dangerous* method.

  ```Ruby
  # bad - there is no matching 'safe' method
  class Person
    def update!
    end
  end

  # good
  class Person
    def update
    end
  end

  # good
  class Person
    def update!
    end

    def update
    end
  end
  ```

* Define the non-bang (safe) method in terms of the bang (dangerous)
  one if possible.

  ```Ruby
  class Array
    def flatten_once!
      res = []

      each do |e|
        [*e].each { |f| res << f }
      end

      replace(res)
    end

    def flatten_once
      dup.flatten_once!
    end
  end
  ```

* When using `reduce` with short blocks, name the arguments `|a, e|`
  (accumulator, element).

* When defining binary operators, name the argument `other`(`<<` and
  `[]` are exceptions to the rule, since their semantics are different).

  ```Ruby
  def +(other)
    # body omitted
  end
  ```

* Prefer `map` over `collect`, `find` over `detect`, `select` over
  `find_all`, `reduce` over `inject` and `size` over `length`. This is
  not a hard requirement; if the use of the alias enhances
  readability, it's ok to use it. The rhyming methods are inherited from
  Smalltalk and are not common in other programming languages. The
  reason the use of `select` is encouraged over `find_all` is that it
  goes together nicely with `reject` and its name is pretty
self-explanatory.

* Don't use `count` as a substitute for `size`. For `Enumerable`
  objects other than `Array` it will iterate the entire collection in
  order to determine its size.

  ```Ruby
  # bad
  some_hash.count

  # good
  some_hash.size
  ```

* Use `flat_map` instead of `map` + `flatten`.
  This does not apply for arrays with a depth greater than 2, i.e.
  if `users.first.songs == ['a', ['b','c']]`, then use `map +
flatten` rather than `flat_map`.
  `flat_map` flattens the array by 1, whereas `flatten` flattens it all
the way.

  ```Ruby
  # bad
  all_songs = users.map(&:songs).flatten.uniq

  # good
  all_songs = users.flat_map(&:songs).uniq
  ```

* Use `reverse_each` instead of `reverse.each`. `reverse_each` doesn't
  do a new array allocation and that's a good thing.

  ```Ruby
  # bad
  array.reverse.each { ... }

  # good
  array.reverse_each { ... }
  ```

