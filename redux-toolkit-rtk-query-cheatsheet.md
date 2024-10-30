# Detailed Redux Toolkit and RTK Query Course Cheatsheet

## 1. Redux Toolkit Intro

- Redux Toolkit: Official, opinionated toolset for efficient Redux development
- Key features:
  - Simplified store setup
  - Reduces boilerplate code
  - Includes useful utilities

### Setting up store

```javascript
import { configureStore } from '@reduxjs/toolkit';
import rootReducer from './reducers';

const store = configureStore({
  reducer: rootReducer,
});

export default store;
```

### Creating a slice

```javascript
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: 0,
  reducers: {
    increment: state => state + 1,
    decrement: state => state - 1,
  },
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

## 2. App Structure & Data Flow

### Folder structure

```javascript
src/
  features/
    counter/
      counterSlice.js
    users/
      usersSlice.js
  app/
    store.js
  index.js
```

### Data flow

1. User interacts with the UI
2. UI dispatches an action
3. Reducer processes the action and updates state
4. UI re-renders based on new state

### Using hooks

```javascript
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from './counterSlice';

function Counter() {
  const count = useSelector(state => state.counter);
  const dispatch = useDispatch();

  return (
    <div>
      <button onClick={() => dispatch(decrement())}>-</button>
      <span>{count}</span>
      <button onClick={() => dispatch(increment())}>+</button>
    </div>
  );
}
```

## 3. Async Logic & Thunks

- Thunk: A function that delays an action until later
- Used for async operations in Redux

### Creating a thunk

```javascript
import { createAsyncThunk } from '@reduxjs/toolkit';

export const fetchUsers = createAsyncThunk(
  'users/fetchUsers',
  async () => {
    const response = await fetch('https://api.example.com/users');
    return response.json();
  }
);
```

### Handling async actions in slice

```javascript
const usersSlice = createSlice({
  name: 'users',
  initialState: { entities: [], loading: 'idle' },
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => {
        state.loading = 'loading';
      })
      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.loading = 'idle';
        state.entities = action.payload;
      });
  },
});
```

## 4. Blog Project

- Implement CRUD operations for a blog using Redux Toolkit

### Post slice example

```javascript
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';

export const fetchPosts = createAsyncThunk('posts/fetchPosts', async () => {
  // Fetch logic here
});

const postsSlice = createSlice({
  name: 'posts',
  initialState: { entities: [], status: 'idle' },
  reducers: {
    postAdded: (state, action) => {
      state.entities.push(action.payload);
    },
    postUpdated: (state, action) => {
      const { id, title, content } = action.payload;
      const existingPost = state.entities.find(post => post.id === id);
      if (existingPost) {
        existingPost.title = title;
        existingPost.content = content;
      }
    },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchPosts.fulfilled, (state, action) => {
        state.status = 'succeeded';
        state.entities = action.payload;
      });
  },
});

export const { postAdded, postUpdated } = postsSlice.actions;
export default postsSlice.reducer;
```

## 5. Performance Optimizations

### Memoizing selectors

```javascript
import { createSelector } from '@reduxjs/toolkit';

const selectPosts = state => state.posts.entities;

export const selectPostsByUser = createSelector(
  [selectPosts, (state, userId) => userId],
  (posts, userId) => posts.filter(post => post.userId === userId)
);
```

### Using `createEntityAdapter`

```javascript
import { createEntityAdapter, createSlice } from '@reduxjs/toolkit';

const postsAdapter = createEntityAdapter({
  sortComparer: (a, b) => b.date.localeCompare(a.date),
});

const postsSlice = createSlice({
  name: 'posts',
  initialState: postsAdapter.getInitialState(),
  reducers: {
    postAdded: postsAdapter.addOne,
    postUpdated: postsAdapter.updateOne,
    postDeleted: postsAdapter.removeOne,
  },
});
```

## 6. RTK Query Intro Project

- RTK Query: Powerful data fetching and caching tool

### Setting up API slice

```javascript
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const api = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: 'https://api.example.com' }),
  endpoints: (builder) => ({
    getPosts: builder.query({
      query: () => 'posts',
    }),
    addPost: builder.mutation({
      query: (post) => ({
        url: 'posts',
        method: 'POST',
        body: post,
      }),
    }),
  }),
});

export const { useGetPostsQuery, useAddPostMutation } = api;
```

### Using RTK Query hooks

```javascript
function PostsList() {
  const { data: posts, isLoading } = useGetPostsQuery();

  if (isLoading) return <div>Loading...</div>;

  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}
```

## 7. Advanced Redux & RTK Query

### Transforming API responses

```javascript
getPosts: builder.query({
  query: () => 'posts',
  transformResponse: (response) => response.map(post => ({
    ...post,
    excerpt: post.content.slice(0, 100) + '...'
  })),
}),
```

### Invalidating cache

```javascript
addPost: builder.mutation({
  query: (post) => ({
    url: 'posts',
    method: 'POST',
    body: post,
  }),
  invalidatesTags: ['Posts'],
}),
```

### Optimistic updates

```javascript
updatePost: builder.mutation({
  query: ({ id, ...patch }) => ({
    url: `posts/${id}`,
    method: 'PATCH',
    body: patch,
  }),
  async onQueryStarted({ id, ...patch }, { dispatch, queryFulfilled }) {
    const patchResult = dispatch(
      api.util.updateQueryData('getPost', id, (draft) => {
        Object.assign(draft, patch);
      })
    );
    try {
      await queryFulfilled;
    } catch {
      patchResult.undo();
    }
  },
}),
```

### Custom error handling

```javascript
export const api = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: 'https://api.example.com' }),
  endpoints: (builder) => ({
    // ... other endpoints
  }),
  refetchOnMountOrArgChange: true,
  refetchOnFocus: true,
  refetchOnReconnect: true,
});
```
