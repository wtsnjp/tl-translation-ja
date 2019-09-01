# Rakefile for wtsnjp/tl-translation-ja
require 'rake/clean'

# cleaning
CLEAN.include(["messages.mo", "ja-merged.po", "README.JA", "readme.ja.html"])

desc "Check the translation file"
task :check do
  # Is the po file valid?
  sh "msgfmt -c ja.po"

  # Is the po file merged with the latest template?
  sh "msgmerge -q ja.po ./translations/messages.pot -o ja-merged.po"
  sh "diff ja.po ja-merged.po"

  # Finale
  puts "All check done. Don't forget to update the revision date!"
end

desc "Build the TeX Live README files"
task :readme do
  # rename the markdown file
  cp "tl-readme-ja.md", "README.JA"

  # generate the HTML version
  sh "pandoc tl-readme-ja.md -o readme.ja.html"
end
