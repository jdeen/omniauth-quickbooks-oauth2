# omniauth-quickbooks-oauth2

[OmniAuth](https://github.com/omniauth/omniauth) strategy for [Intuit QuickBooks](https://quickbooks.intuit.com/).

**Note**: This is a fork of the [original](https://github.com/abeland/omniauth-quickbooks-oauth2) OmniAuth QuickBook oAuth2 strategy. The has
not been updated for a while. This fork unifies somme PRs made against the original repository and also some of my own updates.
## Installation

Add this line to your application's Gemfile:

```ruby
# Gemfile
gem 'omniauth-quickbooks-oauth2', git: 'https://github.com/jdeen/omniauth-quickbooks-oauth2.git'
```

And then run the command:

    $ bundle install

## Usage

In your omniauth initializer file (e.g. `config/initializers/omniauth.rb`), you will want to add the following:

```ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  ...
  provider(
    :quickbooks_oauth2,
    ENV['INTUIT_CLIENT_ID'],
    ENV['INTUIT_CLIENT_SECRET'],
    scope: 'com.intuit.quickbooks.accounting openid profile email phone address',
    sandbox: Rails.env.development?,
  )
  ...
end
```

**NOTE: The above environment variable names and scope are just what I use in my particular project. The environment variables can be named whatever and you should consult [Intuit's documentation](https://developer.intuit.com/docs/00_quickbooks_online/2_build/10_authentication_and_authorization/10_oauth_2.0#/Initiating_the_authorization_request) to figure out which scopes your application should ask for.**

**ALSO NOTE: If the `sandbox` parameter is not explicitly set to `false`, then the strategy will default to using the sandbox endpoints for Intuit's API.**

**ALSO NOTE: If you request the `profile`, `address`, `email`, and/or `phone` scopes, you must also specify the `openid` scope or else Intuit will not allow the OAuth2 dance to happen.**

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/jdeen/omniauth-quickbooks-oauth2.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
