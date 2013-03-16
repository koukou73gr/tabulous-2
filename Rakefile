# -*- encoding: utf-8 -*-

require 'rubygems'
require 'bundler'
Bundler::GemHelper.install_tasks
require 'colored'
require 'rake'
require 'rdoc/task'
require 'rake/testtask'
require 'rspec/core/rake_task'

namespace :spec do
  desc "Run the unit specs"
  RSpec::Core::RakeTask.new(:units) do |t|
    t.pattern = "./spec/lib/**/*_spec.rb"
  end
end

task :test do
  # we cannot load more than one Rails app at a time so running the
  # integration tests this way ensures each Rails app gets its own clean
  # new shell environment
  puts %x{ script/for_all_test_apps bundle exec rake test }
  puts "Running unit specs".magenta
  Rake::Task['spec:units'].invoke
end

task :default => :test

Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_dir = 'rdoc'
  rdoc.title    = 'Test'
  rdoc.options << '--line-numbers' << '--inline-source'
  rdoc.rdoc_files.include('README.rdoc')
  rdoc.rdoc_files.include('lib/**/*.rb')
end
