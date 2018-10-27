<template>
    <div class="radio-component">
        <ul class="radio-list">
            <li v-for="(item, index) in radios" :title="item.label" @click="chosenRadio(index)" :class="{active:index === nowIndex}">{{ item.label }}</li>
        </ul>
    </div>
</template>

<script>
    export default {
        props: {
            radios: {
                type: Array,
                default: [{
                    label: 'test',
                    value: 0
                }]
            }
        },
        data () {
            return {
                nowIndex: 0
            }
        },
        methods: {
            chosenRadio (index) {
                this.nowIndex = index
                this.$emit('on-change', this.radios[index])
            }
        }
    }
</script>

<style scoped>
    .radio-list {
        overflow: hidden;
    }
    .radio-list li {
        float: left;
        margin-right: 10px;
        padding: 0 15px;
        height: 26px;
        line-height: 26px;
        border: 1px solid #ddd;
        cursor: pointer;
    }
    .radio-list :last-child {
        margin-right: 0;
    }
    .radio-list .active {
        color: #fff;
        border-color: #4fc08d;
        background: #4fc08d;
    }
</style>
