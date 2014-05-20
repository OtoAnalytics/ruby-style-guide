* Introduce non-ActiveRecord model classes freely.
* Name the models with meaningful (but short) names without
abbreviations.
* If you need model objects that support ActiveRecord behavior(like
  validation) use the
  [ActiveAttr](https://github.com/cgriego/active_attr) gem.

    ```Ruby
    class Message
      include ActiveAttr::Model

      attribute :name
      attribute :email
      attribute :content
      attribute :priority

      attr_accessible :name, :email, :content

      validates :name, presence: true
      validates :email, format: { with: /\A[-a-z0-9_+\.]+\@([-a-z0-9]+\.)+[a-z0-9]{2,4}\z/i }
      validates :content, length: { maximum: 500 }
    end
    ```

    For a more complete example refer to the
    [RailsCast on the subject](http://railscasts.com/episodes/326-activeattr).

