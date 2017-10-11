---
layout: post
title:      "Facebook-clone Portfolio Project"
date:       2017-10-11 10:13:06 -0400
permalink:  facebook-clone_portfolio_project
---


For this portfolio project I decided to create an app similar to Facebook.  For my has many relationship, I used Facebook likes and posts.  Posts belong to a user when they post on their account and they have many likes.  Likes belong to the user that likes a post.  I made a many to many class and table called PostLikes. When a user creates a post, an instance of Post is created.  When a user likes a post, an Instance of Like is created as well as PostLikes.  PostLikes has the ID of the Post and the ID of the Like.  Through Likes, you can find the individual users that like a post.  Overall, a user can signup with an email, password, date of birth, first name and last name.  This logs them into their profile page which displays their info and an input to post on their wall and the Facebook feed.  They can like a post, unlike a post, edit or delete.  They can’t edit or a delete a post that is not theirs and will be directed to an error page if they try to do so. 

