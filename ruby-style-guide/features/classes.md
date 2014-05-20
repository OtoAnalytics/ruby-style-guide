## Classes & Modules

* Use a consistent structure in your class definitions.

  ```Ruby
  class Person
    # extend and include go first
    extend SomeModule
    include AnotherModule

    # inner classes
    CustomErrorKlass = Class.new(StandardError)

    # constants are next
    SOME_CONSTANT = 20

    # afterwards we have attribute macros
    attr_reader :name

    # followed by other macros (if any)
    validates :name

    # public class methods are next in line
    def self.some_method
    end

    # followed by public instance methods
    def some_method
    end

    # protected and private methods are grouped near the end
    protected

    def some_protected_method
    end

    private

    def some_private_method
    end
  end
  ```

* Don't nest multi line classes within classes. Try to have such nested
  classes each in their own file in a folder named like the containing class.

  ```Ruby
  # bad

  # foo.rb
  class Foo
    class Bar
      # 30 methods inside
    end

    class Car
      # 20 methods inside
    end

    # 30 methods inside
  end

  # good

  # foo.rb
  class Foo
    # 30 methods inside
  end

  # foo/bar.rb
  class Foo
    class Bar
      # 30 methods inside
    end
  end

  # foo/car.rb
  class Foo
    class Car
      # 20 methods inside
    end
  end
  ```

* Prefer modules to classes with only class methods. Classes should be
  used only when it makes sense to create instances out of them.

  ```Ruby
  # bad
  class SomeClass
    def self.some_method
      # body omitted
    end

    def self.some_other_method
    end
  end

  # good
  module SomeClass
    module_function

    def some_method
      # body omitted
    end

    def some_other_method
    end
  end
  ```

* Favor the use of `module_function` over `extend self` when you want
  to turn a module's instance methods into class methods.

  ```Ruby
  # bad
  module Utilities
    extend self

    def parse_something(string)
      # do stuff here
    end

    def other_utility_method(number, string)
      # do some more stuff
    end
  end

  # good
  module Utilities
    module_function

    def parse_something(string)
      # do stuff here
    end

    def other_utility_method(number, string)
      # do some more stuff
    end
  end
  ```

* When designing class hierarchies make sure that they conform to the
  [Liskov Substitution Principle](http://en.wikipedia.org/wiki/Liskov_substitution_principle).

* Try to make your classes as
  [SOLID](http://en.wikipedia.org/wiki/SOLID_\(object-oriented_design\))
  as possible.

* Always supply a proper `to_s` method for classes that represent
  domain objects.

  ```Ruby
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    def to_s
      "#{@first_name} #{@last_name}"
    end
  end
  ```

* Use the `attr` family of functions to define trivial accessors or mutators.

  ```Ruby
  # bad
  class Person
    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end

    def first_name
      @first_name
    end

    def last_name
      @last_name
    end
  end

  # good
  class Person
    attr_reader :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end
  end
  ```

* Avoid the use of `attr`. Use `attr_reader` and `attr_accessor` instead.

  ```Ruby
  # bad - creates a single attribute accessor (deprecated in 1.9)
  attr :something, true
  attr :one, :two, :three # behaves as attr_reader

  # good
  attr_accessor :something
  attr_reader :one, :two, :three
  ```

* Consider using `Struct.new`, which defines the trivial accessors,
  constructor and comparison operators for you.

  ```Ruby
  # good
  class Person
    attr_accessor :first_name, :last_name

    def initialize(first_name, last_name)
      @first_name = first_name
      @last_name = last_name
    end
  end

  # better
  Person = Struct.new(:first_name, :last_name) do
  end
  ````

* Don't extend a `Struct.new` - it already is a new class. Extending it introduces
  a superfluous class level and may also introduce weird errors if the file is
  required multiple times.

* Consider adding factory methods to provide additional sensible ways
  to create instances of a particular class.

  ```Ruby
  class Person
    def self.create(options_hash)
      # body omitted
    end
  end
  ```

* Prefer [duck-typing](http://en.wikipedia.org/wiki/Duck_typing) over inheritance.

  ```Ruby
  # bad
  class Animal
    # abstract method
    def speak
    end
  end

  # extend superclass
  class Duck < Animal
    def speak
      puts 'Quack! Quack'
    end
  end

  # extend superclass
  class Dog < Animal
    def speak
      puts 'Bau! Bau!'
    end
  end

  # good
  class Duck
    def speak
      puts 'Quack! Quack'
    end
  end

  class Dog
    def speak
      puts 'Bau! Bau!'
    end
  end
  ```

* Avoid the usage of class (`@@`) variables due to their "nasty" behavior in inheritance.

  ```Ruby
  class Parent
    @@class_var = 'parent'

    def self.print_class_var
      puts @@class_var
    end
  end

  class Child < Parent
    @@class_var = 'child'
  end

  Parent.print_class_var # => will print "child"
  ```

  As you can see all the classes in a class hierarchy actually share one
  class variable. Class instance variables should usually be preferred
  over class variables.

* Assign proper visibility levels to methods (`private`, `protected`)
  in accordance with their intended usage. Don't go off leaving
  everything `public` (which is the default). After all we're coding
  in *Ruby* now, not in *Python*.

* Indent the `public`, `protected`, and `private` methods as much the
  method definitions they apply to. Leave one blank line above the
  visibility modifier
  and one blank line below in order to emphasize that it applies to all
  methods below it.

  ```Ruby
  class SomeClass
    def public_method
      # ...
    end

    private

    def private_method
      # ...
    end

    def another_private_method
      # ...
    end
  end
  ```

* Use `def self.method` to define singleton methods. This makes the code
  easier to refactor since the class name is not repeated.

  ```Ruby
  class TestClass
    # bad
    def TestClass.some_method
      # body omitted
    end

    # good
    def self.some_other_method
      # body omitted
    end

    # Also possible and convenient when you
    # have to define many singleton methods.
    class << self
      def first_method
        # body omitted
      end

      def second_method_etc
        # body omitted
      end
    end
  end
  ```

