source "https://rubygems.org"

# Specify Ruby version (GitHub Pages supports 2.7+)
ruby "3.1.6"

# GitHub Pages compatible setup
gem "github-pages", group: :jekyll_plugins
gem "webrick", "~> 1.7" # Required for Jekyll with Ruby 3+

# Development tools
group :development do
  gem "rake", "~> 13.0"
  gem "bundler", "~> 2.4"
end

# Additional plugins that work with GitHub Pages
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.15"
  gem "jekyll-seo-tag", "~> 2.8"
  gem "jekyll-sitemap", "~> 1.4"
end

# File watching (for auto-rebuild)
gem "listen", "~> 3.7"

# Web server for local development (compatible versions)
gem "sinatra", "~> 2.2"
gem "rack", "~> 2.2"

# Windows and JRuby compatibility
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]