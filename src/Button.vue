<template>
    <button class="g-button" :class="{[`icon-${iconPosition}`]:true}" @click="$emit('click')">
        <g-icon v-if="icon  &&! loading" :name="icon " class="icon"></g-icon>
        <g-icon class="loading icon" v-if="loading"  name="dengdai"></g-icon>
        <div class="content">
            <slot></slot>
        </div>
    </button>
</template>

<script >
    import Icon from "./Icon";

    export default {
        components:{
            'g-icon':Icon
        },
        props:{
            icon:{},
            loading:{
                type:Boolean,
                default:false,
            },
            iconPosition:{
                type:String,
                default:'left',
                validator(value){
                    return !(value !== 'left' && value !== 'right');
                }
            }
        }
    }
</script>

<style lang='scss' scoped>
    @keyframes spin {
        0%{transform: rotate(0deg)}
        100%{transform: rotate(360deg)}

    }
    .g-button{
        font-size: var(--font-size);
        height: var(--button-height);
        padding: 0 1em;
        border-radius: var(--border-radius);
        border: 1px solid var(--border-color);
        background: var(--button-bg);
        display: inline-flex;
        justify-content: center;
        align-items: center;
        vertical-align: top;  //内联元素无法对齐
        &:hover {
            border-color: var(--border-color-hover);
        }
        &:active {
            background-color: var(--button-active-bg);
        }
        &:focus {
            outline: none;
        }
        > .icon{
            order: 1;
            margin-right: .1em;
        }
        > .content{
            order: 2;
        }
        &.icon-right{
            > .icon{
                order: 2;
                margin-right: 0;
                margin-left: .1em;
            }
            > .content{
                order: 1;
            }
        }

    }
    .loading{
        animation: spin 2s linear infinite;
    }

</style>