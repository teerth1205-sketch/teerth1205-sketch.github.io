---
layout: post
title:      "Rails Portfolio Project"
date:       2020-04-21 18:49:05 -0400
permalink:  rails_portfolio_projectenter_your_title_here
---


This project was another great milestone in my learning career, it implamented a lot of the knowledge learned from the lessons and labs.  Creating the project was a fun and  intense process. I learned to not get completely overwhelmed when something did not work correctly and looked for help when needed. 

The project I created was a task manager, where one can create tasks, either individually or beloging to a project. Projects can have many tasks and tasks can belong to projects.  One of the toughest parts of the project was setting up the associations. 

I finally came to the conclusion that:

Task

belongs to user 
belongs to project

Project

    belongs_to :user
    has_many :tasks, :dependent => :destroy
    has_many :project_users,  :dependent => :destroy
    has_many :users, through: :project_users
    has_many :users_with_tasks, through: :tasks, source: :user 
		
User

has_many :tasks
has_many :project_users
has_many :projects, through: :project_users
has_many :projects_with_tasks, through: :tasks, source: :project

Project_user

belongs_to :project
belongs_to :user

It was tough to get the many to many relationships squared away. Eventually the above worked great. 




