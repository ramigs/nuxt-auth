# nuxt-auth

> Nuxt Strapi Auth

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).


### Usage with @nuxtjs/auth-next module

If you are using the auth-next module you have to change your nuxt.config.js module to work with the strapi user API.

```
strategies: {
  local: {
    token: {
      property: 'jwt',
    },
    endpoints: {
      login: {
        url: 'auth/local',
        method: 'post',
        propertyName: 'jwt',
      },
      user: {
        url: 'users/me',
        method: 'get',
        // no propertyName: false here. Moved to specific user field below
      },
      logout: false,
    },
    user: {
      property: false,
    },
  },
},
```

oi
