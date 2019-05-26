```javascript
const arrayBasedState = {
  posts: [
    { id: "1", title: "", body: "" },
    { id: "2", title: "", body: "" },
    { id: "3", title: "", body: "" }
  ]
}

// Read a record for Array
const postIdToFind = 1;
arrayBasedState.posts.find(post => post.id === postIdToFind);

// Update a record for Array
const newPost = { id: 1, title: "", body: "" };
const newState = arrayBasedState.posts.filter(post => post.id !== newPost.id);
return [ ...newState, newPost];

// Delete a record for Array
const postIdToDelete = 1;
return arrayBasedState.posts.filter(post => post.id !== postIdToDelete);

const objectBasedState = {
  posts: {
    "1": { id: "1", title: "", body: "" },
    "2": { id: "2", title: "", body: "" },
    "3": { id: "3", title: "", body: "" },
  }
}

// Read a record for Object
const postIdToFind = 1;
objectBasedState.posts[postIdToFind];

// Update a record for Object
const newPost = { id: 1, title: "", body: "" };
return { ...newState, [newPost.id]: newPost };

// Delete a record for Object
const postIdToDelete = 1;
delete objectBasedState.posts[postIdToDelete];
objectBasedState
```
