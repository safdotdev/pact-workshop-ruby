source 'https://rubygems.org'

gem 'activesupport'
gem 'httparty'
gem 'rack'
gem 'rackup'
gem 'rake'
gem 'sinatra'

group :development, :test do
  gem 'awesome_print'
  gem 'pry'
  gem 'rspec'

  if ENV['X_PACT_DEVELOPMENT']
    gem 'pact', path: '../pact-ruby'
    gem 'pact-ffi', path: '../pact-ruby-ffi'
    gem 'pact-support', path: '../pact-support'
  else
    gem 'pact', '~> 1.63', git: 'https://github.com/safdotdev/pact-ruby.git', branch: 'feat/ffi'
    gem 'pact-support', '~> 1.16', '>= 1.16.9', git: 'https://github.com/safdotdev/pact-support.git', branch: 'feat/ffi'
    # gem "pact-ffi", "~> 0.4", git: 'https://github.com/safdotdev/pact-ruby-ffi.git', branch: 'feat/ffi'
    gem 'pact_broker-client'
  end
end
