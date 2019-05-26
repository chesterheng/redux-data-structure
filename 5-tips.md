[Five Tips for Working with Redux in Large Applications](https://techblog.appnexus.com/five-tips-for-working-with-redux-in-large-applications-89452af4fdcb)

```javascript
// 1. Store data with an index. Access it with selectors.

const state = {
  "usersById": {
    1: { id: 1, name: "", email: "", phone: "" },
    2: { id: 2, name: "", email: "", phone: "" },
    3: { id: 3, name: "", email: "", phone: "" }
  },
  "selectedUserIds" : [1, 2]
}

const getUsers = ({ usersById }) => {
  return Object.keys(usersById).map((id) => usersById[id]);
}

const users = getUsers(state);
users

const getSelectedUsers = ({ selectedUserIds, usersById }) => {
  return selectedUserIds.map((id) => usersById[id]);
}

const selectedUsers = getSelectedUsers(state);
selectedUsers

// 2. Separate canonical state from view and edit state
const state = {
  "usersById": {
    123: {  
      id: 123,
      name: "Jane Doe",
      email: "jdoe@example.com",
      phone: "555-555-5555",
    }
  },
  "editingUsersById": {
    123: {
      id: 123,
      name: "Jane Smith",
      email: "jsmith@example.com",
      phone: "555-555-5555",
    }
  }
}

// 3. Share state between views judiciously
{
  "usersPage": {
    "usersById": {...},
    ...
  },
  "domainsPage": {
    "domainsById": {...},
    ...
  }
}

// 4. Reuse common reducer functions across state
const initialPaginationState = {
  startElement: 0,
  pageSize: 100,
  count: 0,
};
const paginationReducerFor = (prefix) => {
  const paginationReducer = (state = initialPaginationState, action) => {
    const { type, payload } = action;
    switch (type) {
      case prefix + types.SET_PAGINATION:
        const {
          startElement,
          pageSize,
          count,
        } = payload;
        return Object.assign({}, state, {
          startElement,
          pageSize,
          count,
        });
      default:
        return state;
    }
  };
  return paginationReducer;
};
// example usages
const usersReducer = combineReducers({
  usersData: usersDataReducer,
  paginationData: paginationReducerFor('USERS_'),
});
const domainsReducer = combineReducers({
  domainsData: domainsDataReducer,
  paginationData: paginationReducerFor('DOMAINS_'),
});

// 5. React Integration and Wrap up
const ConnectedComponent = connect(
  (state) => {
    return {
      users: selectors.getCurrentUsers(state),
      editingUser: selectors.getEditingUser(state),
      ... // other props from state go here
    };
  }),
  {
      ...actionCreators, // other normal actions
      setPagination: actionCreatorFactories.setPaginationFor('USERS_'),
  }
)(UsersComponent);
```
