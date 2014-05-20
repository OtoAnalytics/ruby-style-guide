* The model in the mailer spec should be mocked. The mailer should not depend on the model creation.
* The mailer spec should verify that:
  * the subject is correct
  * the sender e-mail is correct
  * the receiver(s) e-mail is stated correctly
  * the e-mail contains the required information

    ```Ruby
    describe SubscriberMailer do
      let(:subscriber) { mock_model(Subscription, email: 'johndoe@test.com', name: 'John Doe') }

      describe 'successful registration email' do
        subject { SubscriptionMailer.successful_registration_email(subscriber) }

        its(:subject) { should == 'Successful Registration!' }
        its(:from) { should == ['info@your_site.com'] }
        its(:to) { should == [subscriber.email] }

        it 'contains the subscriber name' do
          subject.body.encoded.should match(subscriber.name)
        end
      end
    end
    ```

