---
layout: post
title:      "How to set up a CLI Gem "
date:       2017-06-08 10:22:55 -0400
permalink:  how_to_set_up_a_cli_data_gem
---


Step 1. Create a gem with:

		 `$ bundle gem [name]`

Step 2.  Create a file called bin/[name].     
      For this example I will be naming my gem teach. (bin/teach)
			The file should look like this:


```
#!/usr/bin/env ruby

		require "bundler/setup"
		require "teach"

		Teach::CLI.new.call

```
   When you run the app, this is the first thing that will be called.  It is calling the "call" method which we     will make in the lib folder.  

Step 3. Next add a file lib/teach/cli.rb.
     Then add a method named call inside a Teach::CLI class.

	  The file should look like this:

```
     class Teach::CLI

          def call

          end

     end
```

Step 4. Change permissions so that you can run the app with calling "ruby"
         1. cd bin
         2. look at permissions: ls -lah
         3. change permissions with: chmod +x teach

			  Now you can run the app with: ./teach, or from the /teach directory it would be: bin/teach

Step 5. In the cli.rb call method, add puts "Hello World"
         -require "teach/cli" in lib/teach.rb so that your bin/teach file can see your lib/teach/cli file
				 -then call bin/teach

				 You should see "Hello World" in the terminal

Step 6. You can then create other methods in teach/cli and call them inside of the call method.

	     class Teach::CLI

          def call
             puts "Hello World"

             method_2
             method_3
          end

          def method_2
             puts "Hello World from method_2!"
          end

          def method_3
             puts "Hello World from method_3!"
          end

       end

	Step 7. You can create a class and add attributes

	     teach/lesson.rb

			 attr-accessor :title, :num_of_chapters, :teacher

			 def initialize(title, num_of_chapters, teacher)
			     @title = title
					 @num_of_chapters = num_of_characters
					 @teacher = teacher
			  end

	Step 8. From here you can create a class method and use it to send data to the cli.  For instance, if you                want to list all of the lessons, you could make an all_lessons class method that gives all the lesson          instances and their attributes.
