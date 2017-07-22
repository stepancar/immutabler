# immutabler
Javascript library which convert simple mutable reducer's code to immutable

example:

write very simple reducers
```
function user(state, action) {
   if (action.type === 'UPDATE_USER_NAME') {
       state.name = action.name;
   }
}
```
result of compilation

```
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

