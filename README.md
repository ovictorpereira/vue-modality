# vue-modality
A really nice Vue.js modal component.

## Installation
NPM
```bash
$ npm install vue-modality
``` 
Register the component globally...
```js
import Vue from 'vue';
import VueModality from 'vue-modality';

Vue.use(VueModality);
```

... or register the component locally
```js
import VueModality from 'vue-modality';
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
// give your modal a ref and open it by calling
this.$refs.myRef.open();

// or close it by calling
this.$refs.myRef.hide();
```

## Available props

| Prop                             | Type             | Default                | Description              |
|--------------------------|---------------|--------------------|----------------------|
| width         |               String |    400px                   |                                             |
| centered   | Boolean           | false                    | Vertically  centered   |
| overlay    | Boolean           | false     |  |
| title     |         String           |     Modal                |                             |
| title-class   | String           |                        |                                           |
| hide-header     | Boolean           |      false                  |                 |
| hide-footer     | Boolean           |         false               |                 |
| ok-title     | String           |            Ok            |                  |
| ok-disabled     | Boolean           |         false               |                 |
| ok-class     | String           |                        |                 |
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
| open     |          |
| hide     |          |
| ok        |    When the Ok button is pressed      |
| cancel        |    When the Cancel button is pressed      |