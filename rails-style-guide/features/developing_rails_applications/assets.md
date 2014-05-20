Use the [assets pipeline](http://guides.rubyonrails.org/asset_pipeline.html) to leverage organization within
your application.

* Reserve `app/assets` for custom stylesheets, javascripts, or images.
* Use `lib/assets` for your own libraries, that doesn’t really fit into the scope of the application.
* Third party code such as [jQuery](http://jquery.com/) or [bootstrap](http://twitter.github.com/bootstrap/)
  should be placed in `vendor/assets`.
* When possible, use gemified versions of assets (e.g. [jquery-rails](https://github.com/rails/jquery-rails), [jquery-ui-rails](https://github.com/joliss/jquery-ui-rails), [bootstrap-sass](https://github.com/thomas-mcdonald/bootstrap-sass), [zurb-foundation](https://github.com/zurb/foundation)).

