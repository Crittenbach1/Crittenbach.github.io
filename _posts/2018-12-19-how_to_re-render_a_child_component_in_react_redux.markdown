---
layout: post
title:      "How to re-render a child component in React Redux"
date:       2018-12-19 20:44:21 -0500
permalink:  how_to_re-render_a_child_component_in_react_redux
---

During my React Redux review I learned that to re render a child component you either need: 

1. Change the state with setState or
2. Update the store and pass a new updated state to the parent component

For my like button I decided the most efficent solution would be to update the store to re ender everything.

**Step1:**

```
  render() {

      return (
        <div>
           <h3><a href={this.props.article.url}>{this.props.article.title}</a></h3>
           <p>{this.props.article.author}</p>
           <p>{this.props.article.description}</p>
           <p>likes: {this.props.article.likes}</p>
           <button onClick={() => {
            this.updateStateLikes();
           }}> Like </button>
        </div>
      );
  }
```

When the like button is clicked, it calls my updateStateLikes() in my child component with this.updateStateLikes();

**Step2:**

```
  updateStateLikes = () => {

       var newArticle = {
         id: this.props.article.id,
         title: this.props.article.title,
         url: this.props.article.url,
         author: this.props.article.author,
         description: this.props.article.description,
         likes: this.props.article.likes + 1
       };
       this.props.likeArticle(newArticle);

   }
```

The updateStateLikes function then creates a new Article with an updated number of likes.  After that it sends this new article object to the likeArticle Action that was sent to this child component through props.

**Step 3:**

```
import fetch from 'isomorphic-fetch';

export function likeArticle(article) {

  return function(dispatch){
    return fetch(`/api/v1/articles/${article["id"]}`, {
      credentials: "include",
      method: "PUT",
      headers: {
        'Accept': "application/json",
        'Content-Type': "application/json",
      },
      body: JSON.stringify(article)
    })
    .then(res => {
      return res.json()
    }).then(article => {
      console.log(article)
       dispatch({type: 'LIKE_ARTICLE', payload: article})
   })
  }
}
```

This action sends the artice to the rails api at /api/v1/articles/${article["id"]} and then dispatches the article with the type 'LIKE_ARTICLE'

**Step 4:**

Originally I had a seperate likeArticleReducer, but that wasn't neseccary since the Saved Articles Component has it's own reducer and can have a case for 'LIKE_ARTICLE'.  When the Like Article Action sends the type 'LIKE_ARTICLE', this case functon is run. 

```
export default (state = [], action) => {
  switch (action.type) {
    case 'FETCH_SAVED_ARTICLES':
      return action.payload
    case 'LIKE_ARTICLE':
    return state.map(function(article) {
        if (article.id !== action.payload.id) {
          return article } else {
          return action.payload }
      })
    default:
      return state;
  }
}
```

In this case function, we map all the unupdated articles and the updated articles into a new array.  Then we return that array back to savedArticles where it will notice a change in the data causing it to re render.  




