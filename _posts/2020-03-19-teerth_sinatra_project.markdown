---
layout: post
title:      "Teerth Sinatra Project"
date:       2020-03-20 00:15:15 +0000
permalink:  teerth_sinatra_project
---


In the process of creating this project i learned a lot about Databases and coding in ruby as well as html and css. My project is a website that allows you to sign up and log in. Once logged in you can add a run to your runs list and create an event for others to join. Only the creator of the event can delete or update that event. 

I started out by buikding the scaffolding of my app set up as an MVC. I created the models then the database tables. 

```
class Event < ActiveRecord::Base
 has_many :rsvps
 has_many :users, through: :rsvps# add relationships here
 validates_presence_of :time, :location, :description, :date
end
```

the above model has associations, one is the has_many, the event has_many rsvps and the event has many users through rsvps. This is a Many to many relationship. My database table for the events looks like this:


```
class CreateEvents < ActiveRecord::Migration
  def change
     create_table :events do |t|
      t.string :date
      t.string :time 
      t.string :location
      t.string :description 
    end 
  end
end

```

I created 4 different controllers one for each model. To make things seperate. A tough part of creating the controllers was getting certain data from the database using the relationships. This took some trial and error, but eventually i understood that through the many to many relationship, i created a join table allowing access to events to have many users and many rsvps. 

```
class EventController < ApplicationController
  
  get '/events/home' do 
     redirect_if_not_logged_in
    @event = Event.all
    erb :'/landmarks/event'
  end
  
 
  post '/events/new' do
     redirect_if_not_logged_in
     
    @event = Event.new(:time => params["time"], :location => params["location"], :description => params["description"], :date => params["date"])
    if @event.save 
    @user = User.find(session[:user_id])
     @user.events << @event
     redirect '/show'
   else 
     
     @errorss = "You need to input for all fields"
   #  erb :'/landmarks/show'
  end 
  end 
    
   
  post '/events/events/:id/join' do
    redirect_if_not_logged_in
    @event =Event.all
    event = Event.find(params[:id])
     @user = User.find(session[:user_id])
     if @user.events.find_by(:id => event.id)
        @error = "Already Attending"
        erb :'/landmarks/event'
     else
       @user.events << event
       redirect '/show'
     end 
  end
  
  get '/events/:id/update' do 
     redirect_if_not_logged_in
    @event = Event.find(params[:id])
    erb :'landmarks/new'
  end 
  
  patch '/events/:id/update' do 
     redirect_if_not_logged_in
     @event = Event.find(params[:id])
     @rsvp = Rsvp.find_by(:event_id => params[:id])
     if @rsvp.user_id == session[:user_id]
     @event.update(:time => params["time"], :location => params["location"], :date => params["date"], :description => params["description"])
     redirect '/show'
     else
      @error = "you cannot update this event"
     end 
   end 
   
   delete '/events/:id/delete' do 
      redirect_if_not_logged_in
     @event = Event.find(params[:id])
     @rsvp = Rsvp.find_by(:event_id => params[:id])
     if @rsvp.user_id == session[:user_id]
     @event.destroy
     redirect '/show'
     else
       @error1 = "you cannot delete this event"
     end
   end 
   
  delete '/events/:id/remove' do 
     redirect_if_not_logged_in
    @user = User.find(session[:user_id])
    @rsvp = Rsvp.find_by(:user_id => session[:user_id], :event_id => params[:id])
    @rsvp.delete
    redirect '/show'

  end 
  
```

All in all this was a great project experience which allowed me to flex the knowledge that i learned throughout the SInatra curriculum. 
