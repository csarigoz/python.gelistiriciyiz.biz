# -*- encoding: utf-8 -*-
require "bundler/setup"
require "date"
require "time"
require "stringex"
require "yaml"

FILE_DATE_FORMAT = "%Y-%m-%d"
POST_DATE_FORMAT = "%b %d, %Y %H:%M"

NOW = Time.now.strftime(FILE_DATE_FORMAT)

task :default => ["preview"]

desc "Ön izleme / geliştirme sunucusu"
task :preview do
  system "middleman"
end

desc "Test için build"
task :build do
  system "rm -rf build/"
  system "middleman build --verbose"
end

desc "Deploy"
task :deploy do
  system "rm -rf build/"
  system "middleman deploy"
end

desc "Yeni yazı ekle"
task :post, [:post_title, :post_date] do |t, args|
  
  main_config = YAML.load_file('config.yaml')
  main_author = main_config['site']['main_author']
  
  begin
    custom_config = YAML.load_file('config_custom.yaml')
    main_author = custom_config['main_author']
  rescue Exception => e
  end

  post_title = args[:post_title] ? args[:post_title] : "yeni-post"
  post_time = args[:post_date] ? Time.parse(args[:post_date]) : Time.now
  post_file = "source/posts/#{post_time.strftime(FILE_DATE_FORMAT)}-#{post_title.to_url}.md"

  output = []
  output << "---"
  output << "title: \"#{post_title}\""
  output << "date: #{post_time.strftime(POST_DATE_FORMAT)}"
  output << "# tags: tag1,tag2"
  output << "# subtitle: "
  output << "# published: false"
  output << "# cover: "
  output << "author:"
  output << "  name: #{main_author['name']}"
  output << "  email: #{main_author['email']}"
  output << "  link: #{main_author['link']}"
  output << "  bio: #{main_author['bio']}"
  output << "  twitter: #{main_author['twitter']}" if main_author['twitter']
  output << "---"
  File.write post_file, output.join("\n")

  puts "Yeni post edit edilmek için hazır: #{post_file}"
end


desc "Son yazıyı Tweet'le"
task :tweet do
  last_post = Dir['source/posts/*'].last
  meta_data = YAML.load_file(last_post)

  project_domain = "http://python.gelistiriciyiz.biz"
  project_twitter_account = "python_tips_tr"

  post_date = Time.parse(meta_data["date"])
  post_dirdate = post_date.strftime("%Y/%m/%d")
  post_url_path = File.basename(last_post).sub(post_date.strftime("%Y-%m-%d-"), "").split(".").first
  post_url = "#{project_domain}/#{post_dirdate}/#{post_url_path}/"
  post_title = meta_data['title']
  post_tags = meta_data['tags'].split(/ ?, ?/).map{|tag| "##{tag}"}.join(" ")

  status_message = "#{post_title} - #{post_url} #{post_tags}"
  status_message_for_gelistiriciyiz = status_message + " via @#{project_twitter_account}"

  author = meta_data['author'] && meta_data['author']['twitter']
  status_message += " via @#{author}" if author

  if status_message.length <= 140
    system %{
      t set active #{project_twitter_account}
      t update '#{status_message}' && echo '[#{project_twitter_account}] Tweet başarılı...'
    }
  else
    puts "Mesaj 140 karakterden uzun:\n"
  end
  puts status_message

  if status_message_for_gelistiriciyiz.length <= 140
    system %{
      t set active gelistiriciyiz
      t update '#{status_message_for_gelistiriciyiz}' && echo '[gelistiriciyiz] Tweet başarılı...'
    }
  else
    puts "Mesaj 140 karakterden uzun:\n"
  end
  puts status_message_for_gelistiriciyiz
end