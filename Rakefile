require 'rubygems'
require 'rake/gempackagetask'
require 'rubygems/specification'
require 'date'
require 'spec/rake/spectask'

GEM = "dm-appengine"
GEM_VERSION = "0.1.2"
HOMEPAGE = "http://code.google.com/p/appengine-jruby"
SUMMARY = "A DataMapper adapter for Google App Engine"

spec = Gem::Specification.new do |s|
  s.name = GEM
  s.version = GEM_VERSION
  s.platform = Gem::Platform::RUBY
  s.has_rdoc = true
  s.extra_rdoc_files = ["README.rdoc", "LICENSE"]
  s.summary = SUMMARY
  s.description = s.summary
  s.authors = ["Ryan Brown", "David Masover"]
  s.email = ["ribrdb@google.com", "ninja@slaphack.com"]
  s.homepage = HOMEPAGE
  
  s.add_dependency("appengine-apis", ["~> 0.0.17"])
  s.add_dependency("dm-core", ["~> 1.0"])
  s.add_dependency("lexidecimal", ["~> 0.0"])
  
  s.require_path = 'lib'
  s.autorequire = GEM
  s.files = %w(LICENSE README.rdoc Rakefile) + Dir.glob("spec/*.rb") + Dir.glob("lib/**/*.rb")
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
  sh %{sudo gem install pkg/#{GEM}-#{GEM_VERSION}}
end

desc "create a gemspec file"
task :make_spec do
  File.open("#{GEM}.gemspec", "w") do |file|
    file.puts spec.to_ruby
  end
end
