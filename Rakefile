require 'rubygems'
require 'rake/gempackagetask'
require 'rubygems/specification'
require 'date'
require 'spec/rake/spectask'

GEM = 'kafka-rb'
GEM_NAME = 'Kafka Client'
GEM_VERSION = '0.0.5'
AUTHORS = ['Alejandro Crosa']
EMAIL = "alejandrocrosa@gmail.com"
HOMEPAGE = "http://github.com/acrosa/kafka-rb"
SUMMARY = "A Ruby client for the Kafka distributed publish/subscribe messaging service"
DESCRIPTION = "kafka-rb allows you to produce and consume messages using the Kafka distributed publish/subscribe messaging service."

spec = Gem::Specification.new do |s|
  s.name = GEM
  s.version = GEM_VERSION
  s.platform = Gem::Platform::RUBY
  s.has_rdoc = true
  s.extra_rdoc_files = ["LICENSE"]
  s.summary = SUMMARY
  s.description = DESCRIPTION
  s.authors = AUTHORS
  s.email = EMAIL
  s.homepage = HOMEPAGE
  s.add_development_dependency "rspec"
  s.require_path = 'lib'
  s.autorequire = GEM
  s.files = %w(LICENSE README.md Rakefile) + Dir.glob("{lib,tasks,spec}/**/*")
end

task :default => :spec

desc "Run specs"
Spec::Rake::SpecTask.new do |t|
  t.spec_files = FileList['spec/**/*_spec.rb']
  t.spec_opts = %w(-fs --color)
end

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.gem_spec = spec
end

desc "install the gem locally"
task :install => [:package] do
  sh %{sudo gem install pkg/#{GEM_NAME}-#{GEM_VERSION}}
end

desc "create a gemspec file"
task :make_spec do
  File.open("#{GEM}.gemspec", "w") do |file|
    file.puts spec.to_ruby
  end
end

desc "Run all examples with RCov"
Spec::Rake::SpecTask.new(:rcov) do |t|
  t.spec_files = FileList['spec/**/*_spec.rb']
  t.rcov = true
end
