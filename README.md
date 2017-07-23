# immutabler
Javascript library which convert simple mutable reducer's code to immutable

example:

write very simple reducers
```js
function user(state, action) {
   if (action.type === 'UPDATE_USER_NAME') {
       state.name = action.name;
   }
}
```
result of compilation

```js
function user(state, action) {
   if (action.type === 'UPDATE_USER_NAME') {
       return {
           ...state,
           name: action.name
       };
   } else {
      return state;
   }
}
```

Just mutate arrays elements in your reducers
```js
function task(state, action) {
   if (action.type === 'UPDATE_CONTRIBUTOR_NAME') {
      const contributor = state.contributors.find(c => c.id = action.id)[0];
      contributor.name = action.name;
   }
}
```

result of compilation

```js
function task(state, action) {
   if (action.type === 'UPDATE_CONTRIBUTOR_NAME') {
      const contributors = [...state.contributors];
      const oldContributor = contributors.find(c => c.id = action.id)[0];
      const index = contributors.indexOf(oldContributor);
      contributors[index] = {
          ...oldContributor,
          name: action.name
      };
      return {
          ...state,
          contributors
      };
   } else {
       return state;
   }
}
```
