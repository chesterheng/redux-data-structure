Array-based vs Objec-based Redux Store

```javascript
const arrayBasedState = {
  posts: [
    { id: 1, title: "", body: "" },
    { id: 2, title: "", body: "" },
    { id: 3, title: "", body: "" }
  ]
}

// Create a record for Array
const newState = arrayBasedState.posts;
const newPost = { id: 4, title: "", body: "" };
return [ ...newState, newPost];

// Read a record for Array
const postIdToFind = 1;
const postToFind = arrayBasedState.posts.find(post => post.id === postIdToFind);

// Update a record for Array
const newPost = { id: 1, title: "1", body: "" };
const newState = arrayBasedState.posts.filter(post => post.id !== newPost.id);
return [ ...newState, newPost];

// Delete a record for Array
const postIdToDelete = 4;
return arrayBasedState.posts.filter(post => post.id !== postIdToDelete);

const objectBasedState = {
  posts: {
    1: { id: 1, title: "", body: "" },
    2: { id: 2, title: "", body: "" },
    3: { id: 3, title: "", body: "" },
  }
}

// Create a record for Object
const newState = objectBasedState.posts;
const newPost = { id: 4, title: "", body: "" };
return { ...newState, [newPost.id]: newPost };

// Read a record for Object
const postIdToFind = "1";
const postToFind = objectBasedState.posts[postIdToFind];

// Update a record for Object
const newPost = { id: "1", title: "", body: "" };
return { ...newState, [newPost.id]: newPost };

// Delete a record for Object
const newState = objectBasedState.posts;
const postIdToDelete = 1;
delete newState[postIdToDelete];
return newState;
```
