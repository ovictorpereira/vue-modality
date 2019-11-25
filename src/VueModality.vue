<template >
    <transition name="modal-fade">
        <div
            v-if="opened" 
            tabindex="-1"
            class="vue-modality"
            :class="{'vm-centered': centered, 'vm-overlay': overlay}"
            @click.self="backdrop"
            @keyup.esc="esc"
        >
            <div
                class="vue-modality-dialog"
                :style="`width: ${width}`"
                :class="{'margintop': !centered}"
            >
                <header v-if="!hideHeader" >
                    <span class="vm-close-btn" @click="hide"></span>
                    <div class="vm-header" :class="{'vm-header-border': title.length > 0}">
                        <span :class="titleClass">{{title}}</span>
                    </div>
                </header>

                <main
                    class="vm-body"
                    :class="{'vm-text-center':  error || success || textCenter}"
                >
                    <div class="vm-icon vm-error-icon" v-if="error">
                        <div class="vm-inner-error-icon"></div>
                    </div>

                    <div class="vm-icon vm-success-icon" v-if="success">
                        <span class="vm-inner-success-icon">
                            <div class="vm-success-stem"></div>
                            <div class="vm-success-kick"></div>
                        </span>
                    </div>

                    <slot></slot>
                </main>

                <footer v-if="!hideFooter" class="vm-footer">
                    <button
                        v-if="!hideCancel"
                        class="vm-btn vm-cancel-btn"
                        :class="cancelClass"
                        @click.stop="cancel"
                        :disabled="cancelDisabled || okLoading"
                    >
                        {{cancelTitle}}
                    </button>

                    <button
                        v-if="!hideOk"
                        class="vm-btn vm-ok-btn"
                        :class="[okClass, btnLoading]"
                        @click.stop="ok"
                        :disabled="okDisabled"
                    >
                        <span v-if="!okLoading">{{okTitle}}</span>
                        <div v-if="okLoading" class="vm-loader"></div>
                    </button>
                </footer>

            </div>
        </div>
    </transition>
</template>

<script>

export default {
    props: {
        width: {
            type: String,
            default: '400px'
        },
        centered: {
            type: Boolean,
            default: false
        },
        overlay: {
            type: Boolean,
            default: true
        },
        'text-center': {
            type: Boolean,
            default: false
        },
        title: {
            type: String,
            default: 'Modal'
        },
        'title-class': {
            type: String,
            default: ''
        },
        'hide-header': {
            type: Boolean,
            default: false
        },
        'hide-footer': {
            type: Boolean,
            default: false
        },
        'ok-title' : {
            type: String,
            default: 'Ok'
        },
        'ok-disabled': {
            type: Boolean,
            default: false
        },
        'ok-class': {
            type: String,
            default: ''
        },
        'hide-ok': {
            type: Boolean,
            default: false
        },
        'ok-loading': {
            type: Boolean,
            default: false
        },
        'cancel-title': {
            type: String,
            default: 'Cancel'
        },
        'cancel-disabled': {
            type: Boolean,
            default: false
        },
        'cancel-class': {
            type: String,
            default: ''
        },
         'hide-cancel': {
            type: Boolean,
            default: false
        },
        'no-close-on-backdrop': {
            type: Boolean,
            default: false
        },
        'no-close-on-esc': {
            type: Boolean,
            default: false
        },
        error: {
            type: Boolean,
            default: false
        },
        success: {
            type: Boolean,
            default: false
        }
    },
    mounted () {
        window.addEventListener('keyup', e => this.esc(e))
    },
    beforeDestroy () {
        window.removeEventListener('keyup', e => this.esc(e))
    },
    data () {
        return {
            opened: false
        }
    },
    computed: {
        btnLoading () {
            return this.okLoading ? 'vm-btn-loading' : ''
        }
    },
    methods: {
        open () {
            this.$emit('open')
            this.opened = true
        },
        hide () {
            this.$emit('hide')
            this.opened = false
        },
        backdrop () {
            if (!this.noCloseOnBackdrop) this.hide()
        },
        esc (e) {
            if (!this.noCloseOnEsc && e.which === 27) this.hide()
        },
        ok (e) {
            if (this.okLoading) return
            else this.$emit('ok', e)
        },
        cancel (e) {
            this.$emit('cancel', e)
        }
    },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Open+Sans&display=swap');

.vue-modality {
    font-family: "Open Sans", sans-serif;
    color: #555;
    font-size: 14px;
    overflow: hidden;
    line-height: 1.42857143;
    position: fixed;
    height: 100%;
    width: 100%;
    overflow: auto;
    top: 0;
    left: 0;
    display: flex;
    z-index: 9999;
    justify-content: center;
}


@media (max-width: 660px) {
    .vue-modality-dialog {
        width: 96%!important;
        height: 98%!important
    }
}

.vue-modality-dialog {
    position: absolute;
    min-height: 100px;
    max-height: 100vh;
    overflow: auto;
    background: white;
    border-radius: 3px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, .2);
    padding: 13px;
    display: flex;
    flex-direction: column;
}

.vm-overlay{
    background: rgba(0, 0, 0, .3);  
}

.vm-centered {
    align-items: center;
}

.vm-start {
    padding-top: 10px;
    align-items: flex-start;
}

.vm-close-btn {
    position: absolute;
    cursor: pointer;
    top: 16px;
    right: 16px;
    width: 16px;
    height: 16px;
    z-index: 9999;
    opacity: .6;
}

.vm-close-btn:hover {
    opacity: 1;
}

.vm-close-btn:before, .vm-close-btn:after {
    position: absolute;
    content: '';
    height: 2px;
    width: 100%;
    top: 50%;
    left: 0;
    margin-top: -1px;
    background: rgb(83, 83, 83);
    border-radius: 100%;
}

.vm-close-btn:before {
    transform: rotate(45deg);
}

.vm-close-btn:after {
    transform: rotate(-45deg);
}

.vm-btn-loading {
    opacity: .6;
    cursor: default!important;
}

.vm-header {
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 10px;
}

.vm-header-border {
    border-bottom: 1px solid #e9e9e9;
}

.vm-body {
    padding: 16px 0;
    flex: 1;
    /* flex-direction: column;
    display: flex; */
}

/* .vm-body-content-center {
    justify-content: center;
} */

.vm-footer {
    border-top: 1px solid #e9e9e9;
    padding: 13px 0 0 0;
    display: flex;
    justify-content: flex-end;
}

.vm-btn {
    padding: .3rem .75rem;
    border-radius: 2px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    margin-left: 6px;
    border: 0;
    transition: all 0.4s ease;
    cursor: pointer;
    font: inherit!important;
}

.vm-btn:hover {
    opacity: .6;
}

.vm-btn:disabled {
    background: #c1c1c1;
    cursor:default;
}

.vm-btn:disabled:hover {
    opacity: 1;
}

.vm-ok-btn {
    margin-left: 6px;
    border: 0;
    background-color: #2a6ec3;;
    color: white;
}

.vm-cancel-btn {
    background-color: grey;
    color: white;
}

.vm-text-center {
    text-align: center;
}

.margintop {
    margin-top: 10px;
}

.modal-fade-enter,
.modal-fade-leave-active {
    opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
    transition: opacity .5s ease
}

.vm-icon {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background-color: #fff;
    position: relative;
    overflow: hidden;
    display: block;
    margin: 0 auto;
    box-sizing: border-box;
}

.vm-error-icon {
    border: 4px solid #e06565;
    margin-bottom: 12px;
    color: #e06565;
}

.vm-inner-error-icon:after {
    position: relative;
    display: inline-block;
    content: "\D7";
    left: 1px;
    bottom: 24px;
    font-size: 68px;
    animation-name: jump;
    animation-duration: .9s;
}

@keyframes jump {
    0%   {
        bottom: 24px;
    }
    40%  {
        bottom: 36px;
    }
    60% {
         bottom: 24px;
    }
    80% {
        bottom: 30px;
    }
    100% {
         bottom: 24px;
    }
}

.vm-success-icon {
    border: 4px solid #29af18;
    margin-bottom: 12px;
}

.vm-inner-success-icon {
    display:inline-block;
    width: 40px;
    height:40px;
    transform: rotate(45deg);
}

.vm-success-stem {
    position: absolute;
    width: 4px;
    height: 32px;
    background-color: #29af18;
    left: 30px;
    top: 7px;
    border-radius: 2px;
    animation-name: stem;
    animation-duration: .4s;
}

@keyframes stem {
    0%   {
        height: 0px;
        top: 32px;
    }
    49% {
        height: 0px;
        top: 32px;
    }
    100% {
        height: 32px;
        top: 7px;
    }
}

.vm-success-kick {
    position: absolute;
    width: 18px;
    height: 4px;
    background-color: #29af18;
    left: 15px;
    top: 36px;
    border-radius: 2px;
    animation-name: kick;
    animation-duration: 1s;
}

@keyframes kick {
    0%   {
        width: 3px;
    }
    48% {
        width: 18px;
    }
    100% {
        width: 18px;
    }
}

.vm-loader {
    border: 2px solid transparent;
    border-top: 2px solid #f9f9f9;
    border-right: 2px solid #f9f9f9;
    border-bottom: 2px solid #f9f9f9;
    border-radius: 50%;
    width: 14px;
    height: 14px;
    animation: spin 1s linear infinite;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

</style>