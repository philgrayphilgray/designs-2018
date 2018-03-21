# 000_album-collector

> Nuxt.js project

## Build Setup

```bash
# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, checkout the [Nuxt.js docs](https://github.com/nuxt/nuxt.js).

## Create initial design prototype

* Use figma
* Mobile first
* Grayscale

![grayscale prototype of the app](https://s3.amazonaws.com/pg-image-host/github/albumcollector.gif)

## Create basic routing

* Create a dynamic route in pages for `id`

```bash
pages/
├── README.md
├── _id
│   └── edit.vue
├── index.vue
└── new
    └── index.vue
```

## Setup sample data object with Vuex

* Create a new file, `index.js` in the `store` directory
* import `vuex`
* Export `createStore` function that returns a new `Vuex.Store`, passing in the state object and any mutations

```js
import Vuex from 'vuex';

const createStore = () => {
  return new Vuex.Store({
    state: {
      albums: [
        {
          id: '1521567322',
          title: 'Space is the Place',
          artist: 'Sun Ra',
          art: 'http://',
          year: '1973',
          rating: 5
        },
        {
          id: '1521567405',
          title: 'Lanquidity',
          artist: 'Sun Ra',
          art: 'http://',
          year: '1978',
          rating: 5
        }
      ]
    },
    mutations: {
      add(state, newAlbum) {
        state.albums.push(newAlbum);
      }
    }
  });
};

export default createStore;
```

## Create Card Component
