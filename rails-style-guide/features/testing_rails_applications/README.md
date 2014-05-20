* Use just one expectation per example.

    ```Ruby
    # bad
    describe ArticlesController do
      #...

      describe 'GET new' do
        it 'assigns new article and renders the new article template' do
          get :new
          assigns[:article].should be_a_new Article
          response.should render_template :new
        end
      end

      # ...
    end

    # good
    describe ArticlesController do
      #...

      describe 'GET new' do
        it 'assigns a new article' do
          get :new
          assigns[:article].should be_a_new Article
        end

        it 'renders the new article template' do
          get :new
          response.should render_template :new
        end
      end

    end
    ```

* Make heavy use of `describe` and `context`
* Name the `describe` blocks as follows:
  * use "description" for non-methods
  * use pound "#method" for instance methods
  * use dot ".method" for class methods

    ```Ruby
    class Article
      def summary
        #...
      end

      def self.latest
        #...
      end
    end

    # the spec...
    describe Article do
      describe '#summary' do
        #...
      end

      describe '.latest' do
        #...
      end
    end
    ```

* Use [fabricators](http://fabricationgem.org/) to create test
  objects.
* Make heavy use of mocks and stubs

    ```Ruby
    # mocking a model
    article = mock_model(Article)

    # stubbing a method
    Article.stub(:find).with(article.id).and_return(article)
    ```

* When mocking a model, use the `as_null_object` method. It tells the
  output to listen only for messages we expect and ignore any other
  messages.

    ```Ruby
    article = mock_model(Article).as_null_object
    ```

* Use `let` blocks instead of `before(:each)` blocks to create data for
  the spec examples. `let` blocks get lazily evaluated.

    ```Ruby
    # use this:
    let(:article) { Fabricate(:article) }

    # ... instead of this:
    before(:each) { @article = Fabricate(:article) }
    ```

* Use `subject` when possible

    ```Ruby
    describe Article do
      subject { Fabricate(:article) }

      it 'is not published on creation' do
        subject.should_not be_published
      end
    end
    ```

* Use `specify` if possible. It is a synonym of `it` but is more readable when there is no docstring.

    ```Ruby
    # bad
    describe Article do
      before { @article = Fabricate(:article) }

      it 'is not published on creation' do
        @article.should_not be_published
      end
    end

    # good
    describe Article do
      let(:article) { Fabricate(:article) }
      specify { article.should_not be_published }
    end
    ```


* Use `its` when possible

    ```Ruby
    # bad
    describe Article do
      subject { Fabricate(:article) }

      it 'has the current date as creation date' do
        subject.creation_date.should == Date.today
      end
    end

    # good
    describe Article do
      subject { Fabricate(:article) }
      its(:creation_date) { should == Date.today }
    end
    ```


* Use `shared_examples` if you want to create a spec group that can be shared by many other tests.

   ```Ruby
   # bad
    describe Array do
      subject { Array.new [7, 2, 4] }

      context "initialized with 3 items" do
        its(:size) { should eq(3) }
      end
    end

    describe Set do
      subject { Set.new [7, 2, 4] }

      context "initialized with 3 items" do
        its(:size) { should eq(3) }
      end
    end

   #good
    shared_examples "a collection" do
      subject { described_class.new([7, 2, 4]) }

      context "initialized with 3 items" do
        its(:size) { should eq(3) }
      end
    end

    describe Array do
      it_behaves_like "a collection"
    end

    describe Set do
      it_behaves_like "a collection"
    end
    ```

