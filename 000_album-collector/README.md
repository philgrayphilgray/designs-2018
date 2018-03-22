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

## Create Basic Components

Create the following:

* Card
* CardGrid
* Header
* Overlay
* Navigation
* FormInput

Implement:

* Create basic components and implement them in the layout and pages.
* Pass down data from the vuex `$store` as props.
* For example, the `CardGrid` will pass down the album information to each card:

```html
<template lang="pug">
  div
    .card-container
        Card(v-for="(album, index) in $store.state.albums" :album="album" :key="index")

</template>

<script>
import Card from '../components/Card';
export default {
  components: {
    Card
  }
};
```

* The card component will then display that information, transforming for display as needed (immutably, without touching the source data):

```html
<template lang="pug">
  .Card
    img(:src="album.art" :alt="'Album artwork for ' + album.title + ' by ' + album.artist")
    .card-details
      p {{album.title}}
      p {{album.artist}}
      p {{album.year}}
      span
        Star(v-for="(star, index) in stars" :power="star" :key="index")
    .card-controls
    //- controls, edit, delete icons

</template>

<script>
import Star from './Star';
export default {
  data() {
    return {
      stars: []
    };
  },
  props: ['album'],
  components: {
    Star
  },
  beforeMount() {
    this.setStars();
  },
  methods: {
    setStars() {
      for (let i = 1; i <= 5; i++) {
        if (i <= this.album.rating) {
          this.stars.push(true);
        } else {
          this.stars.push(false);
        }
      }
    }
  }
};
</script>
```

## Create the new (POST) form

* Keep the methods input change handlers on the parent component, where the form submit handler is located, and the local state lives
* Create an object in local state with all the form field values, types, and any validation rules

```html
<template lang="pug">
  div.new-form
    h1 Add New Album
    div.art-preview(v-if="newAlbum.art")
      img(:src='newAlbum.art')
    form(@submit.prevent="submitHandler")
      strong.line-through Album Details
      FormInput(v-for="(inputElement, index) in Object.keys(newAlbum)"  :inputName="inputElement" :key="inputElement" @change="inputHandler")
      button.button-submit(type="submit" role="button" aria-labelledby="Submit a new album") save
</template>


<script>
import FormInput from '../../components/FormInput';
export default {
  components: {
    FormInput
  },
  data() {
    return {
      newAlbum: {
        title: '',
        artist: '',
        art: '',
        year: '',
        rating: ''
      }
    };
  },
  methods: {
    inputHandler: function({ input, inputValue }) {
      this.newAlbum[input] = inputValue;
    },
    submitHandler(e) {
      this.$store.commit('add', this.newAlbum);
      e.target.reset();
      this.$router.push({ path: '/' });
    }
  }
};
</script>
```

* Emit events from the child form input components that send a payload of information; listen to these from the parent, using the input change handler as the callback to `@change`
* Use `v-model` to manage state locally in the child component

```html
<!-- FormInput -->
<template lang="pug">
.form-input
    label.sr-only(:for="inputName") {{capitalizedInputName}}
    input(:id="inputName" :name="inputName" :placeholder="capitalizedInputName" v-model="inputValue" @keyup="changeHandler")
</template>

<script>
export default {
  props: ['inputName'],
  data() {
    return {
      inputValue: ''
    };
  },
  computed: {
    capitalizedInputName() {
      const [firstLetter, ...otherLetters] = this.inputName;
      return firstLetter.toUpperCase() + otherLetters.join('');
    }
  },
  methods: {
    changeHandler() {
      this.$emit('change', {
        input: this.inputName,
        inputValue: this.inputValue
      });
    }
  }
};
</script>
```

## Create the navigation overlay

* The navigation is global and can be opened from anywhere, so it's state should be managed in the global vuex `$store`

```js
const createStore = () => {
  return new Vuex.Store({
    state: {
      navToggled: false, // overlay state
      albums: []
    },
    mutations: {
      add(state, newAlbum) {
        state.albums.push(newAlbum);
      },
      toggleNav(state) {
        state.navToggled = !state.navToggled; // toggle; plan to implement explicit open and close mutations
      }
    }
  });
};
```

* Now, the current state of the overlay is accessible from anywhere within the app with `$store.state.navToggled`
* From within a method, we can commit the mutation with `this.$store.commit('toggleNav')`

```html
<template lang="pug">
div(@keyup.esc="toggleOverlay")
    Overlay(v-if="$store.state.navToggled" :toggle="toggleOverlay")
      div(slot="navigation")
        Navigation
    header(role="banner")
        button.menu-button(@click="toggleOverlay" type="button" aria-label="Toggle navigation on" :aria-expanded="$store.state.navToggled")
          span.icon-bar
          span.icon-bar
          span.icon-bar
        .logo
          nuxt-link(to="/")
            img(src="~/assets/svg/logo.svg" alt="Album Collector")

</template>


<script>
import Overlay from '../components/Overlay';
import Navigation from '../components/Navigation';

export default {
  components: { Overlay, Navigation },

  methods: {
    toggleOverlay() {
      this.$store.commit('toggleNav');
    }
  }
};
</script>
```

TODO: ### Implement tabtrapping

## Check Accessibility and other issues

* Install lighthouse

```bash
yarn global add lighthouse
```

* With the app running in dev, run the lighthouse test suite

```bash
lighthouse http://localhost:3000 --view
```

* Read the report and address issues with your code

* Some issues with performance and best practices may be false positives because you're testing a dev build. When you're ready, close dev and start a production build; then run lighthouse

```bash
yarn run build
yarn start
lighthouse http://localhost:3000 --view
```

TODO: ## Add edit and delete controls to Card

TODO: ## Add edit page to Card

TODO: ## Add search, filter, and sorting controls to CardGrid
