* No strings or other locale specific settings should be used in the views,
models and controllers. These texts should be moved to the locale files in
the `config/locales` directory.
* When the labels of an ActiveRecord model need to be translated,
use the `activerecord` scope:

    ```
    en:
      activerecord:
        models:
          user: Member
        attributes:
          user:
            name: "Full name"
    ```

    Then `User.model_name.human` will return "Member" and
    `User.human_attribute_name("name")` will return "Full name". These
    translations of the attributes will be used as labels in the views.

* Separate the texts used in the views from translations of ActiveRecord
attributes. Place the locale files for the models in a folder `models` and
the texts used in the views in folder `views`.
  * When organization of the locale files is done with additional
  directories, these directories must be described in the `application.rb`
  file in order to be loaded.

        ```Ruby
        # config/application.rb
        config.i18n.load_path += Dir[Rails.root.join('config', 'locales', '**', '*.{rb,yml}')]
        ```

* Place the shared localization options, such as date or currency formats, in
files
under
the root of the `locales` directory.
* Use the short form of the I18n methods: `I18n.t` instead of `I18n.translate`
and `I18n.l` instead of `I18n.localize`.
* Use "lazy" lookup for the texts used in views. Let's say we have the
following structure:

    ```
    en:
      users:
        show:
          title: "User details page"
    ```

    The value for `users.show.title` can be looked up in the template
    `app/views/users/show.html.haml` like this:

    ```Ruby
    = t '.title'
    ```

* Use the dot-separated keys in the controllers and models instead of
specifying the `:scope` option. The dot-separated call is easier to read and
trace the hierarchy.

    ```Ruby
    # use this call
    I18n.t 'activerecord.errors.messages.record_invalid'

    # instead of this
    I18n.t :record_invalid, :scope => [:activerecord, :errors, :messages]
    ```

* More detailed information about the Rails i18n can be found in the [Rails
Guides]
(http://guides.rubyonrails.org/i18n.html)

