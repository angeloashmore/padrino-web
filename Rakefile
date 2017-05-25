desc "Update submodule to latest version"
task :submodule_update do
  system "git submodule update --remote --recursive"
end


desc "Updates all blog posts and guides from docs source"
task :update do
  # Update submodule
  sh "git submodule update"
  # Pull latest changes from docs master
  Dir.chdir("docs") { sh "pwd; git stash; git checkout master; git pull origin master; git stash pop; true" }
  # Commit latest revision
  sh "git add docs; git commit -am 'Update docs submodule'; true"
end

desc "Builds the static middleman site to build directory"
task :build => :update do
  sh "middleman build"
end

desc "Update and build and then deploy the site to gh-pages"
task :publish => :build do
  sh "middleman deploy"
end

desc "Staging"
task :staging do
  system "middleman b"
  system "rsync -vru -e \"ssh\" --del build/* xa6195@xa6.serverdomain.org:/home/www/stagingpadrinorb"
  puts '# Please refer to http://stagingpadrinorb.wikimatze.de to visit the staging system'
end

