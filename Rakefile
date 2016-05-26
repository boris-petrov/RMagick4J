require 'rake'

BUILD_FILE = File.join(File.dirname(__FILE__), 'Magick4J', 'build.xml')
JAR_SRC_FILE = File.join(File.dirname(__FILE__), 'Magick4J', 'dist', 'Magick4J.jar')
JAR_DEST_FILE = File.join(File.dirname(__FILE__), 'RMagick4J', 'lib', 'magick4j.jar')

task :default => [:compile, :move, :test, :clean]

task :compile do
  `ant -f #{BUILD_FILE} jar`
  puts 'Compiled magick4j.jar'
end

task :clean do
  `ant -f #{BUILD_FILE} clean`
end

task :move do
  rm_f(JAR_DEST_FILE) 
  mv(JAR_SRC_FILE, JAR_DEST_FILE)
  puts 'Moved jar file to lib folder.'
end

task :work do
  puts `git diff --shortstat 538db96f13ba63fc057b81f9f710554d8f48d84b..HEAD`
end

task :test => [:compile, :move] do
  Dir.chdir 'RMagick4J' do
    puts 'Running tests...'
    system 'rake'
    raise 'Test failed!' unless $? == 0
  end
end
