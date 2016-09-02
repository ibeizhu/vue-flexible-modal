<template>
    <div v-show="visible" class="modal-background" @click="bgClick"></div>
    <div v-el:content class="modal-content" v-show="visible" :transition="transition" :style="bodyStyle">
        <header v-if="!onlyBody" class="modal-content-head">
            <p class="modal-content-title">{{ title }}</p>
            <button class="delete" @click="hide"></button>
        </header>
        <section class="modal-content-body">
            <slot></slot>
        </section>
        <footer v-if="!onlyBody" class="modal-content-foot">
            <a class="button" @click="cancel">{{ cancelText }}</a>
            <a class="button is-primary" @click="ok">{{ okText }}</a>
        </footer>
    </div>
</template>

<script>
    export default {
        props: {
            title: {
                type: String
            },
            okText: {
                type: String,
                default: 'Ok'
            },
            cancelText: {
                type: String,
                default: 'Cancel'
            },
            visible: {
                type: Boolean,
                default: false
            },
            transition: {
                type: String,
                default: 'bounce'
            },
            verify: {
                type: Boolean,
                default: false
            },
            bgClick: {
                type: Boolean,
                default: true
            },
            onlyBody: {
                type: Boolean,
                default: false
            }
        },
        data(){
            return {
                bodyStyle: {}
            }
        },
        watch: {
            visible(){
                if (this.visible) {
                    this.computeStyle();
                }
            }
        },
        ready(){
            this.bind(window,"resize",function(){
                this.computeStyle();
            }.bind(this));
        },
        methods: {
            show () {
                this.visible = true
            },
            hide () {
                this.visible = false
            },
            bgClick(){
                if (this.bgClick) {
                    this.hide();
                }
            },
            ok () {
                if (!this.verify) {
                    this.hide();
                }
                this.$dispatch('MODAL_OK_EVENT')
            },
            cancel () {
                this.hide();
                this.$dispatch('MODAL_CANCEL_EVENT')
            },
            computeStyle(){
                let innerHeight = window.innerHeight - this.$els.content.offsetHeight > 0?window.innerHeight - this.$els.content.offsetHeight:0;
                let innerWidth = window.innerWidth - this.$els.content.offsetWidth > 0?window.innerWidth - this.$els.content.offsetWidth:0;
                this.bodyStyle = {
                    top: `${innerHeight / 2}px`,
                    left: `${innerWidth / 2}px`
                }
            },
            bind(el,eventName,fn){
                if (window.addEventListener) {
                    el.addEventListener(eventName, fn,false);
                } else if (window.attachEvent) {
                    el.attachEvent("on" + eventName, fn);
                }
            }
        }
    }
</script>

<style lang="less" scoped>
    .modal-background {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, .5);
        z-index: 1000;
    }
    button,.button{
        background-color: #fff;
        border: 1px solid #d3d6db;
        border-radius: 3px;
        color: #222324;
        font-size: 14px;
        height: 32px;
        line-height: 24px;
        padding:8px 10px;
        position: relative;
        text-align: center;
        white-space: nowrap;
        cursor: pointer;
        &:hover{
             color: #222324;
             border-color: #aeb1b5;
         }
    }
    .modal-content {
        position: fixed;
        background-color: #fff;
        width: 640px;
        border-radius: 5px;
        z-index: 1001;

        .modal-content-head {
            position: relative;
            padding: 15px;
            background-color: #f5f7fa;
            border-bottom: 1px solid #d3d6db;
            border-top-left-radius:5px;
            border-top-right-radius:5px;
            .delete {
                -webkit-appearance: none;
                background-color: rgba(18, 18, 18, 0.2);
                border: none;
                border-radius: 100%;
                cursor: pointer;
                display: inline-block;
                height: 24px;
                width: 24px;
                position: absolute;
                top: 15px;
                right: 10px;
                &:before {
                    background-color: #fff;
                    content: "";
                    display: block;
                    height: 2px;
                    left: 50%;
                    margin-left: -25%;
                    margin-top: -1px;
                    position: absolute;
                    top: 50%;
                    width: 50%;
                    -webkit-transform: rotate(45deg);
                    transform: rotate(45deg);
                }
                &:after {
                    background-color: #fff;
                    content: "";
                    display: block;
                    height: 2px;
                    left: 50%;
                    margin-left: -25%;
                    margin-top: -1px;
                    position: absolute;
                    top: 50%;
                    width: 50%;
                    -webkit-transform: rotate(-45deg);
                    transform: rotate(-45deg);
                }
                &:hover {
                    background-color: rgba(17, 17, 17, 0.5);
                }
            }
            .modal-content-title {
                color: #222324;
                font-size: 20px;
                line-height: 1;
                margin: 0;
                padding: 0;
            }
        }

        .modal-content-body {
            width: 640px;
            max-height: 600px;
            padding: 20px;
        }

        .modal-content-foot {
            position: relative;
            padding: 15px;
            background-color: #f5f7fa;
            border-top: 1px solid #d3d6db;
            border-bottom-left-radius:5px;
            border-bottom-right-radius:5px;
            .is-primary{
                background-color: #1fc8db;
                border-color: transparent;
                color: #fff;
                margin-left:5px;
                &:hover{
                     background-color: #199fae;
                     border-color: transparent;
                     color: #fff;
                 }
            }
            .button{
                min-width:70px;
            }
        }

    }
    .bounce-transition {
        -webkit-animation-duration: .5s;
        animation-duration: .5s;
        -webkit-animation-fill-mode: both;
        animation-fill-mode: both;
    }

    .bounce-enter {
        animation-name: bounceIn;
    }

    .bounce-leave {
        animation-name: bounceOut;
    }

    @-webkit-keyframes bounceIn {
        from, 20%, 40%, 60%, 80%, to {
            animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
        }

        0% {
            opacity: 0;
            transform: scale3d(.3, .3, .3);
        }

        20% {
            transform: scale3d(1.1, 1.1, 1.1);
        }

        40% {
            transform: scale3d(.9, .9, .9);
        }

        60% {
            opacity: 1;
            transform: scale3d(1.03, 1.03, 1.03);
        }

        80% {
            transform: scale3d(.97, .97, .97);
        }

        to {
            opacity: 1;
            transform: scale3d(1, 1, 1);
        }
    }

    @keyframes bounceIn {
        from, 20%, 40%, 60%, 80%, to {
            animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
        }

        0% {
            opacity: 0;
            transform: scale3d(.3, .3, .3);
        }

        20% {
            transform: scale3d(1.1, 1.1, 1.1);
        }

        40% {
            transform: scale3d(.9, .9, .9);
        }

        60% {
            opacity: 1;
            transform: scale3d(1.03, 1.03, 1.03);
        }

        80% {
            transform: scale3d(.97, .97, .97);
        }

        to {
            opacity: 1;
            transform: scale3d(1, 1, 1);
        }
    }

    @-webkit-keyframes bounceOut {
        20% {
            transform: scale3d(.9, .9, .9);
        }

        50%, 55% {
            opacity: 1;
            transform: scale3d(1.1, 1.1, 1.1);
        }

        to {
            opacity: 0;
            transform: scale3d(.3, .3, .3);
        }
    }

    @keyframes bounceOut {
        20% {
            transform: scale3d(.9, .9, .9);
        }

        50%, 55% {
            opacity: 1;
            transform: scale3d(1.1, 1.1, 1.1);
        }

        to {
            opacity: 0;
            transform: scale3d(.3, .3, .3);
        }
    }
</style>
