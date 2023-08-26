# Rakefile for wtsnjp/tl-translation-ja
require 'rake/clean'

# cleaning
CLEAN.include(["messages.mo", "ja-merged.po", "README.JA", "readme.ja.html"])

desc "Rsync the translations dir"
task :rsync do
  sh "rsync -a --delete --exclude=.svn tug.org::tldevsrc/Master/tlpkg/translations/ ./translations/"
end

desc "Merge the translation file"
task :merge => :rsync do
  sh "msgmerge -q ja.po ./translations/messages.pot -o ja-merged.po"
end

desc "Take the diff between the latest translation and that in distribution"
task :diff => :merge do
  sh "colordiff -u ./translations/ja.po ja-merged.po || true"
end

desc "Check the translation file"
task :check => :merge do
  # is the po file valid?
  sh "msgfmt -c ja.po"

  # is the po file merged with the latest template?
  sh "diff -q ja.po ja-merged.po"

  # finale
  puts "All check passed. Don't forget to update the revision date!"
end

desc "Build the TeX Live README files"
task :readme do
  # rename the markdown file
  cp "tl-readme-ja.md", "README.JA"

  # generate the HTML version
  sh "pandoc tl-readme-ja.md -o readme.ja.html"
end
