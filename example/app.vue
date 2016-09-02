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

<style lang="less" scoped>
    .control {
        position: relative;
        text-align: left;
    }
    button{
        -moz-appearance: none;
        -webkit-appearance: none;
        -webkit-box-align: center;
        -ms-flex-align: center;
        align-items: center;
        background-color: #fff;
        border: 1px solid #d3d6db;
        border-radius: 3px;
        color: #222324;
        display: -webkit-inline-box;
        display: -ms-inline-flexbox;
        display: inline-flex;
        font-size: 14px;
        height: 32px;
        -webkit-box-pack: start;
        -ms-flex-pack: start;
        justify-content: flex-start;
        line-height: 24px;
        padding-left: 8px;
        padding-right: 8px;
        position: relative;
        vertical-align: top;
        -webkit-box-pack: center;
        -ms-flex-pack: center;
        justify-content: center;
        padding-left: 10px;
        padding-right: 10px;
        text-align: center;
        white-space: nowrap;
    }
    .label {
        color: #222324;
        display: block;
        font-weight: 700;
    }
    input{
        -moz-appearance: none;
        -webkit-appearance: none;
        -webkit-box-align: center;
        -ms-flex-align: center;
        align-items: center;
        background-color: #fff;
        border: 1px solid #d3d6db;
        border-radius: 3px;
        color: #222324;
        display: -webkit-inline-box;
        display: -ms-inline-flexbox;
        display: inline-flex;
        font-size: 14px;
        height: 32px;
        -webkit-box-pack: start;
        -ms-flex-pack: start;
        justify-content: flex-start;
        line-height: 24px;
        padding-left: 8px;
        padding-right: 8px;
        position: relative;
        vertical-align: top;
        box-shadow: inset 0 1px 2px hsla(0,0%,7%,.1);
    }
</style>