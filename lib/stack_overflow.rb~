require 'httparty'
require 'json'
require 'question'
require 'answer'
require 'cgi'

module API
  module StackOverflow
    include HTTParty
    @@API_KEY = nil
    @@URL_START = "https://api.stackexchange.com/2.1/"
    @@URL_END = "&site=stackoverflow"
    @@filter = "&filter=!bULULYbOAl(mz*"

    def self.API_KEY=(value)
      @@API_KEY = value
    end

    def self.API_KEY
      @@API_KEY
    end

    
    def self.get_user_description(user_id)
	result = get(@@URL_START + "users/#{user_id}?key=#{@@API_KEY}&order=desc&sort=reputation" + @@URL_END + @@filter)
	return nil if result["items"].nil?
	result["items"]["about_me"]
    end

    def self.get_user_by_name(user_name, options={})
	user_name = user_name.split(" ").join("%20")
	page = options[:page] || 1
        pagesize = options[:pagesize] || 30
	result = get(@@URL_START + "users?key=#{@@API_KEY}&page=#{page}&pagesize=#{pagesize}&order=desc&sort=reputation&inname=#{user_name}" + @@URL_END + @@filter)
	return nil if result["items"].nil?
        result["items"]
    end
    
    def self.get_all_users(options={})
      key = @@API_KEY
      page = options[:page] || 1
      pagesize = options[:pagesize] || 30
      result = get(@@URL_START + "users?key=#{@@API_KEY}&page=#{page}&pagesize=#{pagesize}" + @@URL_END + @@filter)
      return nil if result["items"].nil?
      result["items"]
    end

    def self.get_user(user_id)
      result = get(@@URL_START + "users/#{user_id}?key=#{@@API_KEY}&order=desc&sort=reputation" + @@URL_END + @@filter)
      return nil if result["items"].nil?
      result["items"].first
    end

    def self.get_users(user_ids,options={})
      user_id = user_ids.join(";").to_s
      page = options[:page] || 1
      pagesize = options[:pagesize] || 30
      result = get(@@URL_START + "users/#{user_id}?key=#{@@API_KEY}&page=#{page}&pagesize=#{pagesize}&order=desc&sort=reputation" + @@URL_END + @@filter)
      return nil if result["items"].nil?
      result["items"]
    end
      

    def self.get_user_questions(user_id,options={})
      page = options[:page] || 1
      pagesize = options[:pagesize] || 30
      result = get(@@URL_START + "users/#{user_id}/questions?key=#{@@API_KEY}&page=#{page}&pagesize=#{pagesize}&order=desc&sort=votes" + @@URL_END + "&filter=!bULULQb5)kbksz")
      return nil if result["items"].nil?
      result["items"]
    end

    def self.get_user_answers(user_id, options={})
      page = options[:page] || 1
      pagesize = options[:pagesize] || 30
      result = get(@@URL_START + "users/#{user_id}/answers?key=#{@@API_KEY}&page=#{page}&pagesize=#{pagesize}&order=desc&sort=votes" + @@URL_END + "&filter=!bULULfcU_Ma1As")
      return nil if result["items"].nil?
      result["items"]
    end


    def self.get_user_tags(user_id)
      result = get(@@URL_START + "users/#{user_id}/tags?key=#{@@API_KEY}&order=desc&sort=popular" + @@URL_END)
      return nil if result["items"].nil?
      result["items"]
    end

    def self.get_tags(options={})
      page = options[:page] || 1
      pagesize = options[:pagesize] || 30 
      result=get(@@URL_START + "tags?key=#{@@API_KEY}&page=#{page}&page_size=#{pagesize}&order=desc&sort=popular" + @@URL_END)
      return nil if result["items"].nil?
      result["items"]
    end

    def self.get_tag_synonyms(tag)
      result = get(@@URL_START + "tags/#{tag}/synonyms?key=#{@@API_KEY}&order=desc&sort=creation" + @@URL_END)
      ans = Array.new
      syn = result["items"]
      return nil if syn.nil?
      syn.each{ |t|
	ans.push(t["from_tag"])
      }
      return ans.join(" ")
    end
    def self.get_question_tags(id)
      result = get(@@URL_START + "questions/#{id}?key=#{@@API_KEY}&order=desc&sort=activity" + @@URL_END)
      return nil if result.nil?
      return result["items"][0]["tags"]
    end
  end
end

