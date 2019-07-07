require 'json'
require 'erb'
require 'fileutils'

task :build do
  FileUtils.rm_rf("html")
  FileUtils.mkdir("html")

  @venues = {}
  Dir["data/*"].each do |file|
    content = JSON.parse(File.read(file))
    # TODO: actually map those to objects
    @venues[File.basename(file, ".*")] = content
  end

  # render index.html
  result = ERB.new(File.read("views/index.erb")).result(binding)
  File.write("html/index.html", result)

  @venues.each do |key, venue|
    @venue = venue
    result = ERB.new(File.read("views/detail.erb")).result(binding)
    File.write(File.join("html", "#{key}.html"), result)
  end
  
end
