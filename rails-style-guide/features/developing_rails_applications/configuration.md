* Put custom initialization code in `config/initializers`. The code in
  initializers executes on application startup.
* Keep initialization code for each gem in a separate file
  with the same name as the gem, for example `carrierwave.rb`,
  `active_admin.rb`, etc.
* Adjust accordingly the settings for development, test and production
  environment (in the corresponding files under `config/environments/`)
  * Mark additional assets for precompilation (if any):

        ```Ruby
        # config/environments/production.rb
        # Precompile additional assets (application.js, application.css, and all non-JS/CSS are already added)
        config.assets.precompile += %w( rails_admin/rails_admin.css rails_admin/rails_admin.js )
        ```

* Keep configuration that's applicable to all environments in the `config/application.rb` file.
* Create an additional `staging` environment that closely resembles
the `production` one.

