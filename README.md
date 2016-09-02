# vue-flexible-modal

# Overview
a flexible modal component by vue.js

# Installation
First, install `vue-flexible-modal` from npm:
```bash
$ npm install vue-flexible-modal
```

Then import it:
```javascript
import Modal from 'vue-flexible-modal';
```

# Usage
Please view the example folder


# API
| Option             | Description                                                      | Value                  | Default  |
|--------------------|------------------------------------------------------------------|------------------------|----------|
| title            | Modal Tile                                  | String                | ''  |
| okText          | ok button text                              | String |          | 'ok'  |
| cancelText         | cancel button text                             | String |          | 'cancel' |
| visible             | control modal show or hide                                     | Boolean                 |     'false'     |
| transition              | modal show or hide animation/transition                | String                | 'bounce'  |
| verify         | if need verify form data when click ok button                           | Boolean                 |    'false'      |
| bgClick | the switch to hide modal by clicking background      | Boolean                | 'true'  |
| onlyBody  | hide the modal head and foot,only show body content | Boolean                | 'false'  |
