require 'book_builder/book_builder'



namespace :book do
  desc "compile files from the current directory and publish to all available formats"
  task :publish do
    html()
    plain_text()
    log 'Done!'
  end
  
  desc "Outstanding TODO's"  
  task :todo do
    # man this is messy! -bj
    `grep --exclude=\*.svn\* -nr TODO book/source/`.each_line do |line|
      path, line, *note = line.split ':'
      note = note.join(':').strip
      path.gsub!(/[^\d]+/, '.').gsub!(/^\.|\.$/,'')
      
      log "#{note} (Section #{path}, Line #{line})"
    end
  end

  namespace :publish do
    desc "compile files from the current directory into html"
    task :html do
      log 'Publishing HTML...'
      html
      log 'Done!'
    end
  
    desc "compile files from the current directory into pain text"
    task :text do
      log 'Publishing plain text...'
      plain_text
      log 'Done!'
    end
  end
  
  desc "prepare a structure for publishing to"
  task :prepare do
    log 'Preparing a publishing structure...'
    book = default_book
    book.prepare!
    log 'Done!'
  end
end

# crate an html output
def html
  book = default_book
  log 'Processing HTML format...'
  book.html!
end

# crate a plain text output
def plain_text
  book = default_book
  log 'Processing Plain Text format...'
  book.plain_text!
end


# this is here as a helper so we can send messages somewhere other than stdout at a later date if we want to.
def log(msg='')
  puts msg
end

def default_book
  BookBuilder::Book.new('merb_book','./book/', :markdown)
end



