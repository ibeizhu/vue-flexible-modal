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
                if(!this.modal.text){
                    alert('Text can not be empty');
                    return false;
                }
                this.modal.visible = false;
            },
            MODAL_CANCEL_EVENT(){

            },
            MODAL_OK_EVENT2(){
                // TODO your logic
            },
            MODAL_CANCEL_EVENT2(){

            }
        },
        data:{
            modal:{
                title:'I am modal title',
                visible:false,
                text:''
            },
            modal2:{
                title:'I am modal2 title',
                visible:false,
                text:'',
                bgStyle:{
                    'z-index':'4000'
                },
                contentStyle:{
                    'width':'300px'
                }
            }
        },
        methods:{
            onShowModal1(){
                this.modal.visible = !this.modal.visible;
            },
            onShowModal2(){
                this.modal2.visible = !this.modal2.visible;
            }
        }
    };

</script>

<template>
    <div>
        <br>
        <br>
        <button @click="onShowModal1">Click Show Modal1</button>
        <br>
        <br>
        <label class="label">Use as MessageBox</label>
        <br>
        <button @click="onShowModal2">Click Show Modal2</button>
        <modal :title="modal.title" :visible.sync="modal.visible" :verify="true">
            <label class="label">Slot Area,write your code in here</label>
            <p class="control">
                <label class="label">Name:</label>
                <input class="input" type="text" v-model="modal.text" placeholder="Your name">
            </p>
        </modal>

        <modal :title="modal2.title" :visible.sync="modal2.visible" :bg-click="false" :verify="true" :bg-style="modal2.bgStyle" :content-style="modal2.contentStyle" :only-body="true" :modal-id="1">
            <label class="label">Welcome to use vue-flexible-modal</label>
            <p class="control">
                <button class="ok" @click="onShowModal2">ok</button>
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
    .ok{
        float: right;
    }
</style>