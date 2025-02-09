# Storybook Addon Next Router

Use Next.js Router in your Storybook stories.

This is a fork of the `storybook-addon-next-router` library. It fix the compatibility with next v11.2+.

## Versions

- Use `storybook-addon-next-router` 1.x if you're using storybook 5.x
- Use `storybook-addon-next-router` 2.x if you're using storybook 6.x
- Use `@gogaille/storybook-addon-next-router` 4.x if you're using storybook 6.x and next 11.2+

## As a decorator in a story

```jsx
import { withNextRouter } from 'storybook-addon-next-router';
import MyComponentThatHasANextLink from '../component-that-has-a-next-link';

export default {
  title: 'My Story',
  decorators: [withNextRouter], // not necessary if defined in preview.js
};

// if you have the actions addon
// you can click the links and see the route change events there
export const Example = () => <MyComponentThatHasANextLink />;

Example.story = {
  parameters: {
    nextRouter: {
      path: '/profile/[id]',
      asPath: '/profile/lifeiscontent',
      query: {
        id: 'lifeiscontent',
      },
    },
  },
};
```

## Usage in `preview.js`

### Simple

```js
import { withNextRouter } from 'storybook-addon-next-router';

export decorators = [
  withNextRouter
];
```

### Custom

```js
import { withNextRouter } from 'storybook-addon-next-router';

export decorators = [
  withNextRouter({
    path: '/', // defaults to `/`
    asPath: '/', // defaults to `/`
    query: {}, // defaults to `{}`
    push() {} // defaults to using addon actions integration, can override any method in the router
  })
];
```

If you set up `withNextRouter` in preview, it will not need to be added to the `decorators` key in each story, consider doing this if you have a lot of stories that depend on Apollo.

Read more about the options available for next/router at https://nextjs.org/docs/api-reference/next/router

## Example App

To see real world usage of how to use this addon, check out the example app:

https://github.com/lifeiscontent/realworld
