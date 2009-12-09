# Usage:  rake com.example.MonkeyShines
#  Source goes under ./src
#  Classes end up under ./target
 
require 'rake/clean'
 
libs = FileList["lib/*"]
libs << "target"
JavaClassPaths = libs.join(":")
 
# regex should weed out anything containing "/", i.e. paths
rule(/^[^\/]+\.\w/ => lambda {|tn| "src/#{tn.gsub(".", "/")}.class"} ) do |t|
  # system(command)
end
 
rule ".class" => [".java", "target"] do |t|
  puts command = "javac -classpath #{JavaClassPaths} #{t.source} -d target"
  system(command)
  target_path = t.name.sub("src/", "target/").sub(/\.class$/, "")
  puts command = "javap -c -v #{target_path} > #{target_path}.bc"
  system(command)
  puts command = "xxd #{target_path}.class > #{target_path}.hex"
end
 
desc "make directories, or whatever"
task :setup => ["src", "lib"]
 
directory "target"
directory "src"
directory "lib"
 
CLEAN.include("target")