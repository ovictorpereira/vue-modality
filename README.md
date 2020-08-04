# vue-modality
A really nice Vue.js modal component.
#### [Demo](https://ovictorpereira.github.io/vue-modality/ "Demo")
#### [Sandbox](https://jsfiddle.net/ovictorpereira/hceu6mz4/15/ "Sandbox")

## Installation
NPM
```bash
$ npm install vue-modality
``` 
Register the component globally...
```js
import Vue from 'vue'
import VueModality from 'vue-modality'

Vue.use(VueModality)
```

... or register it locally
```js
import VueModality from 'vue-modality'
export default {
  components: {
    VueModality
  }
};
```

## Usage
```html
<vue-modality ref="myRef" title="My Title" centered>
  body content
</vue-modality>
```
```js
// give your modal a ref and open it by calling:
this.$refs.myRef.open()

// or close it by calling:
this.$refs.myRef.hide()

```

## CDN
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>vue-modality</title>
    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
    <script src="https://unpkg.com/vue-modality"></script>
</head>
<body>
    <h1>Vue-Modality</h1>
    <div id="app">
        <button @click="$refs.example.open()">
            Open the modal
        </button>
        <vue-modality ref="example" @ok="$refs.example.hide()" @cancel="$refs.example.hide()" title="Modal" centered>
            Use the footer buttons to close the modal
        </vue-modality>
    </div>

    <script>
        const vueApp = new Vue({el: '#app'});
    </script>
</body>
</html>
```

## Available props

| Prop                             | Type             | Default                | Description              |
|--------------------------|---------------|--------------------|----------------------|
| width         |               String |    400px                   |                                             |
| centered   | Boolean           | false                    | Vertically  centered   |
| overlay    | Boolean           | false     |  |
| text-center         |               Boolean |    false                   |                                             |
| title     |         String           |     Modal                |                             |
| title-class   | String           |                        |                                           |
| hide-header     | Boolean           |      false                  |                 |
| hide-footer     | Boolean           |         false               |                 |
| ok-title     | String           |            Ok            |                  |
| ok-disabled     | Boolean           |         false               |                 |
| ok-class     | String           |                        |                 |
| ok-loading     | Boolean           |        false          |      Shows the loading icon           |
| hide-ok     | Boolean           |      false                  |       Hides the ok button          |
| cancel-title     | String           |          Cancel              |                |
| cancel-disabled     | Boolean           |         false               |                 |
| cancel-class     | String           |                        |                 |
| hide-cancel     | Boolean           |      false                  |       Hides the cancel button          |
| no-close-on-backdrop     | Boolean           |      false                  |               |
| no-close-on-esc     | Boolean           |      false                  |               |
| error     | Boolean           |      false                  |      Shows error icon         |
| success     | Boolean           |      false                  |      Shows success icon         |

## Events
| Event    |  Description |
|----------|--------------|
| open     |  When you open the modal       |
| hide     |   When you hide the modal       |
| ok        |    When the Ok button is pressed      |
| cancel        |    When the Cancel button is pressed      |