#!/usr/bin/env rake
# frozen_string_literal: true

require 'bundler/gem_tasks'

task default: :test

# ==========================================================
# Packaging
# ==========================================================

GEMSPEC = eval(File.read('pygments.rb.gemspec'))

require 'rubygems/package_task'

# ==========================================================
# Testing
# ==========================================================

require 'rake/testtask'
Rake::TestTask.new 'test' do |t|
  t.test_files = FileList['test/test_*.rb']
end

# ==========================================================
# Benchmarking
# ==========================================================

task :bench do
  sh 'ruby bench.rb'
end

# ==========================================================
# Cache lexers
# ==========================================================

# Write all the lexers to a file for easy lookup
task :lexers do
  sh 'ruby cache-lexers.rb'
end

task(:test).enhance([:lexers])
task(:build).enhance([:lexers])

# ==========================================================
# Vendor
# ==========================================================

namespace :vendor do
  file 'vendor/pygments-main' do |f|
    sh "pip install --target=#{f.name} pygments"
  end

  task :clobber do
    rm_rf 'vendor/pygments-main'
  end

  desc 'update vendor/pygments-main'
  task update: [:clobber, 'vendor/pygments-main']
end
