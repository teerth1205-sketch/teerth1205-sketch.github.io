---
layout: post
title:      "Teerth's CLI project"
date:       2020-02-14 20:55:24 +0000
permalink:  teerths_cli_project
---


This project was really helpfull in solidifying the material learned in the previos lessons and labs. My project was an app that scrapes the IMDB website of top 100 movies. It first asks for input when the app is initailly opened. You can type in 1 or 2(if you were already in the app and want to view your watchlist after navigating back to the home menu). Type 1 and outputted to the CLI is a list of the top 100 IMDB movies. from here you can select a movie by typing in the number of the movie. After this the output will be a screen of info on the specific movie you selected. At this point you can either go back, go home add the movie to your watchlist or view your watchlist.  That basically sums up the usage of my app. 

```

class Scrape
  
  def get_page
    @doc = Nokogiri::HTML(open("https://www.imdb.com/list/ls068082370/"))
      
  end 
  
  def get_content
  self.get_page.css(".lister-item-content")
    
  end 
  
  def assign_content
    
    self.get_content.each do |item|
      list = List.new
      list.title  = item.css(".lister-item-header").text.gsub(/\s+/, " ")
      list.genre = item.css(".genre").text.gsub(/\s+/, "")
      list.paragraph = item.css("p").text.split("\n")[8]
      list.rating = item.css("p").text.split("\n")[1].gsub(/\s+/, "")
      list.runtime = item.css("p").text.split("\n")[3].gsub(/\s+/, " ")
  
    
    end 
  end


end 
```

Above is the code for the scraper I created. I had some trouble trying to find the right css selectors for the specific parts of the movie info, however, i got through it.  In the code a new instance of the List class is created each time adding the specific info of the movie into the List object. Below is the List class holding all the info on the movies in a class variable @@all. All this info is then accssessed with the CLI class, which acts as my controller. All in all the project used all that i learned from previous labs and lessons and formed everything nicely in one place.  

```
class List
  attr_accessor :title, :genre, :paragraph, :rating, :runtime
  @@all = []
  
  def initialize
    @@all << self 
  end 
  
  def self.all 
    @@all
 
  end 
  
  
end 
```
