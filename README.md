# vue-flexible-modal
a flexible modal component by vue.js

[Live Demo](http://imoment.vip/business/modal/index)

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
Please view the detail code in example folder

```html
<script>
    import Modal from 'vue-flexible-modal';
    export default {
        el: '#page',
        components: {
            Modal
        },
        events:{
            MODAL_OK_EVENT(){
                // you can set modal show or hide with the variable 'this.modal.visible' manually
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
| title            | Modal Title                                  | String                | 'Modal'  |
| okText          | ok button text                              | String |        'ok'  |
| cancelText         | cancel button text                             | String |          'cancel' |
| visible             | control the modal show or hide(primary key)     | Boolean     |     'false'     |
| transition      | modal show or hide with your custom animation/transition   | String      | 'bounce'  |
| verify         | if need verify form data when click ok button     | Boolean                 |    'false'      |
| bgClick | the switch for hiding modal by clicking background      | Boolean                | 'true'  |
| onlyBody  | hide the modal head and foot,only show body content | Boolean                | 'false'  |
| bgStyle | custom set background style     | Object                | {}  |
| contentStyle  | custom set content style | Object                | {}  |



# Usage Example

simple
```html
<modal :title="modal.title" :visible.sync="modal.visible" :verify="true">
    <label class="label">Slot Area,write your code in here</label>
    <p class="control">
        <label class="label">Name:</label>
        <input class="input" type="text" v-model="modal.text" placeholder="Your name">
    </p>
</modal>
```

Use api params to configure a MessageBox

```html
<modal :title="modal2.title" :visible.sync="modal2.visible" :bg-click="false" :verify="true" :bg-style="modal2.bgStyle" :content-style="modal2.contentStyle" :only-body="true" :modal-id="1">
    <label class="label">Welcome to use vue-flexible-modal</label>
    <p class="control">
        <button class="ok" @click="onShowModal2">ok</button>
    </p>
</modal>
```
