---
layout: post
title:      "How to add a date a time to your website with javascript and jQuery "
date:       2018-09-04 18:33:30 +0000
permalink:  how_to_add_a_date_a_time_to_your_website_with_javascript_and_jquery
---


1. Create a new rails app
       Rails new show_date
   2. Create the home page 
     
    class ApplicationController < ActionController::Base

    def home 
    
     end 
  
    end

——

   Create a root route to the home page

    Rails.application.routes.draw do
       For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html

       root to: "application#home"

    end
   

———

  Create a view folder application with a home.html.erb file. 

———


  3. Add this to your gemfile and run bundle install
      gem 'jquery-rails'

      And references to the jquery scripts in your layouts/application.html.erb file header
      
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.0.11/handlebars.min.js"></script>


4. Add a div with a class name of date-time to the home page 
    

<div class="date-time">
</div>


5. Add an internal javascript to test out your code on the page first.

   It should use a document ready function that will load when the page runs. Inside the
Function, add some text to the div with a class name of date-time ( .date-time).
  Load the page to make sure the text is showing.

    <script type="text/javascript" charset="utf-8">
$(document).ready(function() {

  $('.date-time').html("date and time");

});
 </script>


6. Create a variable that holds the date and time. You can get this data by calling the new Date($.now()); function

     var dt = new Date($.now());
 
     Add it to the page with this:
 
       $('.date-time').html(dt);

  You should see it displayed on the page as:
  
     Sat Aug 25 2018 01:34:20 GMT-0400 (EDT)

  This doesn’t look so good so we will create another variable that extracts the time:
    
      var time = dt.getHours() + ":" + dt.getMinutes() + ":" + dt.getSeconds();

  And another that extracts the date:

     var date = "Now: " + dt.getDate() + "/"
               + (dt.getMonth()+1)  + "/"
               + dt.getFullYear();
  
  Display this on the page by changing your code to:

     $('.date-time').html(date + " at " + time);

      7.  Now that we have out code working, lets make an external javascript file for it for cleaner code.

     In assets/javascripts/application.js, copy and paste just this part of the javascript code:
     
$(document).ready(function() {

  var dt = new Date($.now());
  var time = dt.getHours() + ":" + dt.getMinutes() + ":" + dt.getSeconds();
  var date = "Now: " + dt.getDate() + "/"
               + (dt.getMonth()+1)  + "/"
               + dt.getFullYear();

  $('.date-time').html(date + " at " + time);

});


Your home page should work the same way but the date time is being called from your assets folder and being rendered in the .date-time div in your home.html.erb file.

