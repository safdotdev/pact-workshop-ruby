# encoding: utf-8

require 'rubygems'
require 'bundler'

begin
  Bundler.setup(:default, :development)
rescue Bundler::BundlerError => e
  $stderr.puts e.message
  $stderr.puts "Run `bundle install` to install missing gems"
  exit e.status_code
end

require 'rake'
require 'pact/tasks'
require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec)

task :default => [:spec]

$:.unshift 'lib'

desc 'Run the client'
task :run_client do
  require 'client'
  require 'ap'
  ap Client.new.process_data
end

require 'pact/tasks/verification_task'

task :start_provider do
  system 'bundle exec rackup --pid provider.pid -D'
end

task :stop_provider do
  system 'kill $(cat provider.pid)'
end

Pact::VerificationTask.new(:foobar_pact) do |pact|
  pact.provider_base_url 'http://localhost:9292', pact_helper: './spec/spec_helper.rb'
end
task 'pact:verify:foobar' do
  Rake::Task['start_provider'].execute
  Rake::Task['pact:verify:foobar_pact'].execute
ensure
  Rake::Task['stop_provider'].execute
end
