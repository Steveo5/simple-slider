
Simply built vue image slider.<br /> 

# Project structure

In **src** sub-folder we have VueJS application including
1. entry.js
2. SimpleSlider.vue

# Setup

1. `npm  i simpleslider`
2. `In your entry point (where Vue is included, such as app.js/main.js) add the code below`
```
import SimpleSlider from 'simpleslider'
Vue.use(SimpleSlider)
```

#### Project requirements
1. none

#### Props
There is a number of props to use, you must set the images

1. `images` (array of objects) e.g. [ { title: 'test', url: '/some/url', id: 1, text: 'Lorem ipsum, etc, etc' }, { title: 'test 2', url: '/some/url2', id: 2 }]
2. `interval` (number) how often to automatically change images, in milliseconds, defaults to 15000


Any problems can be reported to https://github.com/Steveo5/simple-slider
