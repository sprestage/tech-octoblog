source "https://rubygems.org"
ruby '2.0.0'

group :development do
  gem 'rake'
  gem 'jekyll'
  gem 'rdiscount'
  gem 'pygments.rb'
  gem 'RedCloth'
  gem 'haml'
  gem 'compass'
  gem 'sass'
  gem 'sass-globbing'
  gem 'rubypants'
  gem 'rb-fsevent'
  gem 'liquid'
  gem 'directory_watcher'
end

gem 'sinatra', '~> 1.4.2'
gem 'stringex', '~> 1.4.0'

group :production do
  gem 'newrelic_rpm'
end

group :development, :test do
# Figaro for removing secret keys from github
  gem 'figaro'
end
