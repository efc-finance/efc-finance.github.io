require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"

GITHUB_REPONAME=ENV["GITHUB_REPONAME"]
GITHUB_PUBLISH_BRANCH=ENV["GITHUB_PUBLISH_BRANCH"]

namespace :site do
  desc "Generate blog files"
  task :generate do
    Jekyll::Site.new(Jekyll.configuration({
      "source"      => ".",
      "destination" => "_site"
    })).process
  end

  desc "Remove files not needed for your site"
  task :clean do
    unwanted_files = ['_site/Gemfile.lock','_site/Vagrantfile','_site/Gemfile.lock',
        '_site/Rakefile','_site/README.md','_site/CNAME','_site/vssh','_site/Gemfile']
    unwanted_files.each { |i| if File.exist?(i); File.delete(i); end  }
    FileUtils.rm_rf('_site/script')
  end

  desc "Publish blog to gh-pages branch"
  task :publish => [:clean] do
    Dir.mktmpdir do |tmp|
      cp_r "_site/.", tmp
      Dir.chdir tmp
      system "git init"
      system "git add ."
      message = "Site updated at #{Time.now.utc}"
      system "git commit -m #{message.inspect}"
      system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
      system "git push origin master:refs/heads/#{GITHUB_PUBLISH_BRANCH} --force"
    end
  end
end