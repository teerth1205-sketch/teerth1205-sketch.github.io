---
layout: post
title:      "Rails and Javascript project"
date:       2020-05-20 04:31:39 +0000
permalink:  rails_and_javascript_project
---


This project really tested my ability to absorb the information taught in the lessons and labs. For my project I created an instagram clone, called "Snapstagram" which is a single page appilcation that allows the users to upload an image file and then write comments on the images presented. This project tested all of the requirements. It has a rails API and a Javascript frontend. 

One of the main challenges i faced during the process was getting the upload of the picture to work and persist in the database. For this i used active storage. Which allows the photo model i created to have attached to it an image file stored with acrtive storage. The tough part was figuring out that we needed a serializer to make the diplaying of the image more straightforward. We inherited from the active model serializer. 



```
class PhotoSerializer < ActiveModel::Serializer
  attributes :id, :image_url, :title
  has_many :comments
  belongs_to :user
  
end
```
