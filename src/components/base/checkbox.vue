<template>
    <div class="checkbox-component">
        <ul class="checkbox-list">
            <li v-for="(item, index) in checkboxs" :title="item.label" @click="chosenCheckbox(index)" :class="{active: checkActive(index)}">{{ item.label }}</li>
        </ul>
    </div>
</template>

<script>
    import _ from 'lodash'
    export default {
        props: {
            checkboxs: {
                type: Array,
                default: [{
                    label: 'test',
                    value: 0
                }]
            }
        },
        data () {
            return {
                nowIndexes: [0]
            }
        },
        methods: {
            chosenCheckbox (index) {
                if (this.nowIndexes.indexOf(index) === -1) {
                    this.nowIndexes.push(index)
                } else {
                    this.nowIndexes = _.remove(this.nowIndexes, (idx) => {
                        return idx !== index
                    })
                }
                let nowObjArray = _.map(this.nowIndexes, (idx) => {
                    return this.checkboxs[idx]
                })
                this.$emit('on-change', nowObjArray)
            },
            checkActive (index) {
                return this.nowIndexes.indexOf(index) !== -1
            }
        }
    }
</script>

<style scoped>
    .checkbox-list {
        overflow: hidden;
    }
    .checkbox-list li {
        float: left;
        margin-right: 10px;
        padding: 0 15px;
        height: 26px;
        line-height: 26px;
        border: 1px solid #ddd;
        cursor: pointer;
    }
    .checkbox-list :last-child {
        margin-right: 0;
    }
    .checkbox-list .active {
        color: #fff;
        border-color: #4fc08d;
        background: #4fc08d;
    }
</style>
