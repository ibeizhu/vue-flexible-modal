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

```html
<script>
    import Modal from '../src/Modal';

    export default {
        el: '#page',
        components: {
            Modal
        },
        events:{
            MODAL_OK_EVENT(){
                // you can manual set modal show or hide use this.modal.visible
                // this.modal.visible = false;
            },
            MODAL_CANCEL_EVENT(){

            }
        },
        data:{
            modal:{
                title:'I am modal title',
                visible:false,
                text:''
            }
        },
        methods:{
            onShowModal(){
                this.modal.visible = !this.modal.visible;
            }
        }
    };

</script>

<template>
    <div>
        <button @click="onShowModal">Click Show Modal</button>
        <modal :title="modal.title" :visible.sync="modal.visible" :bg-click="false" :verify="true">
            <p class="control">
                <label class="label">Name:</label>
                <input class="input" type="text" v-model="modal.text" placeholder="Your name">
            </p>
        </modal>
    </div>
</template>
```

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
