task :default => :build

task :build do
  system("jekyll")
end

task :new do
  throw "No title given" unless ARGV[1]
  title = ""
  ARGV[1..ARGV.length - 1].each { |v| title += " #{v}" }
  title.strip!
  now = Time.now
  path = "_posts/#{now.strftime('%F')}-#{title.downcase.gsub(/[\s\.]/, '-').gsub(/[^\w\d\-]/, '')}.md"
  
  File.open(path, "w") do |f|
    f.puts "---"
    f.puts ""
    f.puts "layout: post"
    f.puts "title: \"#{title}\""
    f.puts "date: #{now.strftime('%F %T')}"
    f.puts "category: "
    f.puts "tags:"
    f.puts "  - "
    f.puts ""
    f.puts "---"
    f.puts ""
    f.puts ""
  end
  
  `open -a "Sublime Text 2" #{path}`
  exit
end

task :css do
  require "sass"
  contents = IO.read("css/site.scss").gsub(/^\-{3}\n.*?\-{3}/, "")
  
  File.open("_site/css/site.css", "w") do |f|
    f.write Sass::Engine.new(contents, :syntax => :scss, :style => :compressed).render
  end
end
