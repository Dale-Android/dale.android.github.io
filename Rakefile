require 'rake'
require 'yaml'

SOURCE = "."
CONFIG = {
  'posts' => File.join(SOURCE, "_posts"),
  'post_ext' => "md",
}

# Usage: rake post title="A Title"
desc "Begin a new post in #{CONFIG['posts']}"
task :post do
  abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])
  title = ENV["title"] || "new-post"
  # slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  slug = title.downcase.strip.gsub(' ', '-') # 去掉，以支持中文
  anyTime = ENV["time"].to_i
  time = anyTime != 0 ? Time.at(anyTime) : Time.now
  filename = File.join(CONFIG['posts'], "#{time.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  now = time

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "date: \"#{now.inspect}\""
    post.puts "description: #{ENV["desc"]}"
    post.puts "img: #{ENV["img"]}"
    post.puts "tags: [#{ENV["tags"]}]"
    post.puts "mathjax: true"
    post.puts "---"
  end
end # task :post
