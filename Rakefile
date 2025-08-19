require "bundler/setup"

# Configuration
GITHUB_REPONAME = "www.subnet.co.za"

desc "Serve the site locally"
task :serve do
  puts "Starting Jekyll server..."
  system "bundle exec jekyll serve --watch --drafts --port 4000"
end

desc "Build the site"
task :build do
  puts "Building site..."
  system "bundle exec jekyll build"
end

desc "Clean up generated files"
task :clean do
  puts "Cleaning up..."
  system "bundle exec jekyll clean"
  system "rm -rf .sass-cache"
end

desc "Build and serve the site"
task :dev => [:build, :serve]

desc "Deploy to GitHub Pages"
task :deploy => :build do
  puts "Deploying to GitHub Pages..."
  
  # Check if we're on the right branch
  current_branch = `git rev-parse --abbrev-ref HEAD`.strip
  puts "Current branch: #{current_branch}"
  
  # Build the site
  system "bundle exec jekyll build"
  
  # Check if build was successful
  unless File.directory?("_site")
    puts "ERROR: Jekyll build failed - _site directory not found"
    exit 1
  end
  
  puts "Site built successfully"
  puts "Commit and push your changes to deploy to GitHub Pages"
end

desc "Create a new post"
task :new_post, [:title] do |t, args|
  title = args[:title] || "New Post"
  slug = title.downcase.gsub(/[^\w\s-]/, '').gsub(/[\s_-]+/, '-')
  date = Time.now.strftime('%Y-%m-%d')
  filename = "_posts/#{date}-#{slug}.md"
  
  if File.exist?(filename)
    puts "ERROR: Post already exists at #{filename}"
    exit 1
  end
  
  puts "Creating new post: #{filename}"
  
  File.open(filename, 'w') do |f|
    f.puts "---"
    f.puts "layout: post"
    f.puts "title: \"#{title}\""
    f.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M:%S %z')}"
    f.puts "categories: []"
    f.puts "tags: []"
    f.puts "---"
    f.puts ""
    f.puts "Your content here..."
  end
  
  puts "Post created! Edit: #{filename}"
end

desc "Check site health"
task :check do
  puts "Checking site health..."
  
  # Check if bundle is up to date
  puts "Checking bundle..."
  system "bundle check" or system "bundle install"
  
  # Check if Jekyll can build
  puts "Testing Jekyll build..."
  success = system "bundle exec jekyll build --destination /tmp/jekyll-test-build"
  
  if success
    puts "✓ Site health check passed"
  else
    puts "✗ Site health check failed"
    exit 1
  end
end

desc "Update dependencies"
task :update do
  puts "Updating dependencies..."
  system "bundle update"
  puts "Dependencies updated!"
end

desc "Show available tasks"
task :help do
  puts "Available tasks:"
  puts "  rake serve     - Serve the site locally on http://localhost:4000"
  puts "  rake build     - Build the site"
  puts "  rake clean     - Clean up generated files"
  puts "  rake deploy    - Build and prepare for GitHub Pages deployment"
  puts "  rake new_post[title] - Create a new post"
  puts "  rake check     - Check site health"
  puts "  rake update    - Update dependencies"
  puts "  rake help      - Show this help"
end

# Default task
task :default => :help