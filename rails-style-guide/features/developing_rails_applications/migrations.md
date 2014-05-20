* Keep the `schema.rb` (or `structure.sql`) under version control.
* Use `rake db:schema:load` instead of `rake db:migrate` to initialize
an empty database.
* Use `rake db:test:prepare` to update the schema of the test database.
* Enforce default values in the migrations themselves instead of in
  the application layer.

    ```Ruby
    # bad - application enforced default value
    def amount
      self[:amount] or 0
    end
    ```

    While enforcing table defaults only in Rails is suggested by many
    Rails developers, it's an extremely brittle approach that
    leaves your data vulnerable to many application bugs.  And you'll
    have to consider the fact that most non-trivial apps share a
    database with other applications, so imposing data integrity from
    the Rails app is impossible.

* Enforce foreign-key constraints. While ActiveRecord does not support
them natively, there some great third-party gems like
[schema_plus](https://github.com/lomba/schema_plus) and [foreigner](https://github.com/matthuhiggins/foreigner).

* When writing constructive migrations (adding tables or columns), use
  the new Rails 3.1 way of doing the migrations - use the `change`
  method instead of `up` and `down` methods.


    ```Ruby
    # the old way
    class AddNameToPeople < ActiveRecord::Migration
      def up
        add_column :people, :name, :string
      end

      def down
        remove_column :people, :name
      end
    end

    # the new prefered way
    class AddNameToPeople < ActiveRecord::Migration
      def change
        add_column :people, :name, :string
      end
    end
    ```

* Don't use model classes in migrations. The model classes are
constantly evolving and at some point in the future migrations that
used to work might stop, because of changes in the models used.

