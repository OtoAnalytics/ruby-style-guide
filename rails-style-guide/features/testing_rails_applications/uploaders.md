* What we can test about an uploader is whether the images are resized correctly.
Here is a sample spec of a [carrierwave](https://github.com/jnicklas/carrierwave) image uploader:

    ```Ruby

    # rspec/uploaders/person_avatar_uploader_spec.rb
    require 'spec_helper'
    require 'carrierwave/test/matchers'

    describe PersonAvatarUploader do
      include CarrierWave::Test::Matchers

      # Enable images processing before executing the examples
      before(:all) do
        UserAvatarUploader.enable_processing = true
      end

      # Create a new uploader. The model is mocked as the uploading and resizing images does not depend on the model creation.
      before(:each) do
        @uploader = PersonAvatarUploader.new(mock_model(Person).as_null_object)
        @uploader.store!(File.open(path_to_file))
      end

      # Disable images processing after executing the examples
      after(:all) do
        UserAvatarUploader.enable_processing = false
      end

      # Testing whether image is no larger than given dimensions
      context 'the default version' do
        it 'scales down an image to be no larger than 256 by 256 pixels' do
          @uploader.should be_no_larger_than(256, 256)
        end
      end

      # Testing whether image has the exact dimensions
      context 'the thumb version' do
        it 'scales down an image to be exactly 64 by 64 pixels' do
          @uploader.thumb.should have_dimensions(64, 64)
        end
      end
    end

    ```

