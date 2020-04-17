<template>
    <div class="mt-3 bg-white card p-3 ">
        <div class="pb-3 d-flex flex-wrap  ai-center"
        :class="{'border-bottom' : !plain ,'pb-3':!plain}">
            <i class="iconfont" :class="`icon-${icon}`"></i>
            <div class="ml-2">
                <strong>{{title}}</strong>
            </div>
        </div>
        <i class="iconfont icon-menu" v-if="!plain"></i>
        <div class="card-body pt-3">
            <slot></slot>
        </div>
    </div>
</template>

<style lang="scss">
    @import "../assets/scss/_variables.scss";

    .card {
        border-bottom: 1px solid $border-color;
    }
</style>

<script>
    export default {
        props: {
            title: {
                type: String,
                required: true
            },
            icon: {
                type: String,
                required: true
            },
            plain: { type: Boolean }
        }
    }
</script>