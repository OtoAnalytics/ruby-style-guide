* Signal exceptions using the `fail` method. Use `raise` only when
  catching an exception and re-raising it (because here you're not
  failing, but explicitly and purposefully raising an exception).

  ```Ruby
  begin
    fail 'Oops'
  rescue => error
    raise if error.message != 'Oops'
  end
  ```

* Don't specify `RuntimeError` explicitly in the two argument version of `fail/raise`.

  ```Ruby
  # bad
  fail RuntimeError, 'message'

  # good - signals a RuntimeError by default
  fail 'message'
  ```

* Prefer supplying an exception class and a message as two separate
  arguments to `fail/raise`, instead of an exception instance.

  ```Ruby
  # bad
  fail SomeException.new('message')
  # Note that there is no way to do `fail SomeException.new('message'), backtrace`.

  # good
  fail SomeException, 'message'
  # Consistent with `fail SomeException, 'message', backtrace`.
  ```

* Never return from an `ensure` block. If you explicitly return from a
  method inside an `ensure` block, the return will take precedence over
  any exception being raised, and the method will return as if no
  exception had been raised at all. In effect, the exception will be
  silently thrown away.

  ```Ruby
  def foo
    begin
      fail
    ensure
      return 'very bad idea'
    end
  end
  ```

* Use *implicit begin blocks* where possible.

  ```Ruby
  # bad
  def foo
    begin
      # main logic goes here
    rescue
      # failure handling goes here
    end
  end

  # good
  def foo
    # main logic goes here
  rescue
    # failure handling goes here
  end
  ```

* Mitigate the proliferation of `begin` blocks by using
  *contingency methods* (a term coined by Avdi Grimm).

  ```Ruby
  # bad
  begin
    something_that_might_fail
  rescue IOError
    # handle IOError
  end

  begin
    something_else_that_might_fail
  rescue IOError
    # handle IOError
  end

  # good
  def with_io_error_handling
     yield
  rescue IOError
    # handle IOError
  end

  with_io_error_handling { something_that_might_fail }

  with_io_error_handling { something_else_that_might_fail }
  ```

* Don't suppress exceptions.

  ```Ruby
  # bad
  begin
    # an exception occurs here
  rescue SomeError
    # the rescue clause does absolutely nothing
  end

  # bad
  do_something rescue nil
  ```

* Avoid using `rescue` in its modifier form.

  ```Ruby
  # bad - this catches exceptions of StandardError class and its descendant classes
  read_file rescue handle_error($!)

  # good - this catches only the exceptions of Errno::ENOENT class and its descendant classes
  def foo
    read_file
  rescue Errno::ENOENT => ex
    handle_error(ex)
  end
  ```

* Don't use exceptions for flow of control.

  ```Ruby
  # bad
  begin
    n / d
  rescue ZeroDivisionError
    puts 'Cannot divide by 0!'
  end

  # good
  if d.zero?
    puts 'Cannot divide by 0!'
  else
    n / d
  end
  ```

* Avoid rescuing the `Exception` class.  This will trap signals and calls to
  `exit`, requiring you to `kill -9` the process.

  ```Ruby
  # bad
  begin
    # calls to exit and kill signals will be caught (except kill -9)
    exit
  rescue Exception
    puts "you didn't really want to exit, right?"
    # exception handling
  end

  # good
  begin
    # a blind rescue rescues from StandardError, not Exception as many
    # programmers assume.
  rescue => e
    # exception handling
  end

  # also good
  begin
    # an exception occurs here

  rescue StandardError => e
    # exception handling
  end
  ```

* Put more specific exceptions higher up the rescue chain, otherwise
  they'll never be rescued from.

  ```Ruby
  # bad
  begin
    # some code
  rescue Exception => e
    # some handling
  rescue StandardError => e
    # some handling
  end

  # good
  begin
    # some code
  rescue StandardError => e
    # some handling
  rescue Exception => e
    # some handling
  end
  ```

* Release external resources obtained by your program in an ensure block.

  ```Ruby
  f = File.open('testfile')
  begin
    # .. process
  rescue
    # .. handle error
  ensure
    f.close unless f.nil?
  end
  ```

* Favor the use of exceptions for the standard library over
  introducing new exception classes.

