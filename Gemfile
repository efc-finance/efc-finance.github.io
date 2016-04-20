source 'https://rubygems.org'

require 'json'
require 'open-uri'

gem 'therubyracer'
gem 'html-proofer'

versions = JSON.parse(open('https://pages.github.com/versions.json').read)
gem 'github-pages', versions['github-pages']

