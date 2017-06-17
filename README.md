# vue-bootstrap-modal

> A Vue.js project to wrap bootstrap modal in to Vue component.

## Usage

### Install
```bash
npm i -S crip-vue-bootstrap-modal
```

### Setup
```javascript
import Vue from 'vue'
import CripModal from 'crip-vue-bootstrap-modal'

// Install component in to Vue instance
Vue.use(CripModal)
```

### Create modal 
```vue
<template>
    <crip-modal 
        @hidden="modalHidden" 
        @shown="modalShown" 
        size="sm" 
        :close="close"
    >
        <span slot="title">Modal Title</span>
        
        <div class="modal-body">
          Content should be here
          <button class="btn btn-danger" @click="closeModal">&times;</button>
        </div>
    </crip-modal>
</template>

<script>
  export default {
    data () {
      return {
        // open modal by default while it is mounting
        close: false
      }
    },
    
    methods: {
      closeModal () {
        this.close = true
      },
      modalHidden () {
        console.log('modal now is hidden')
      },
      modalShown () {
        console.log('modal now is visible')
      }
    },
    
  }
</script>
```

## Build Setup

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

## Release steps

```bash

# Commit sources to git repository
> git add -A
> git commit -m "[build] v$VERSION"

#update version number
> npm version $VERSION --message "[release] v$VERSION"

# Build assets
> npm run build

# publish
> git push
> npm publish
```
