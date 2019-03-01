*NodeJS Nested Array Data*

This week I learned how to nest arrays in mongodb data and list it in a Nodejs recipe app.

*Step 1* 

First I created a Schema for recipe steps:

```
let stepSchema = new Schema({
   description: {
     type: String,
     required: true
   }
});
```

*Step 2* 

I then added a steps array to the recipe Schema, refering to the Step Schema.

```
let recipeSchema = new Schema;

    recipeSchema.add({
      steps: [stepSchema],
      name: {
        type: String,
        required: true
      }
    });
```

*Step 3*

To send new data to the router I needed to create a form with the action="/recipes/{{_id}}/steps" and method="post".
The id is then used in the route to find which recipe to update with a new step.

```

  <form action="/recipes/{{_id}}/steps" method="post">
            <input type="text" name="description" >
            <button type="submit">Add</button>
          </form>

```

*Step 4*

In routes.js I added a new router that with create a new step and save it in it's recipe's step array.

1. finds the recipe by it's id
2. creates a new step object with the given description
3. checks whether recipe.steps is an array, if not creates one and adds new step
4. saves updated recipe and redirects back to index with new data to list 

```
router.post('/recipes/:id/steps', function(req, res){

  let recipeId = req.params.id;

  Recipe.findById(recipeId)
    .exec()
    .then(function(recipe) {
      var step = {description: req.body.description};

      if (Array.isArray(recipe.steps)) {
          recipe.steps.push(step);
          console.log(recipe);
      } else {
          recipe.steps = [];
          recipe.steps.push(step);
      }
      
    recipe
   .save()
    }).then(function(result){
       res.redirect('/');
    })

  });

```

*Step 5* 

I added an ordered list to each recipe thats lists it's steps.

In mustache to list a nested array, you add another {{#steps}} just likew the outsdie one which was {{#recipes}}.
Then add the <li></li> with object attributes you want to display. ( {{description}} )

```
      <ol>
            {{#steps}}
              <li>
                 {{description}}
              </li>
            {{/steps}}
     </ol>

```
