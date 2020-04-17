<template>
    <div class="page-article " v-if="model">
        <!-- 头 -->
        <div class="d-flex py-3 px-2 border-bottom">
            <div class="iconfont icon-news"></div>
            <strong class="flex-1 text-blue pl-2">{{model.title}}</strong>
            <div class="text-grey fs-xs">{{model.createAt}}2019-06-19</div>
        </div>
        <!-- 中 -->
        <div v-html="model.body" class="px-3 fs-lg body"></div>
        <!-- 底 -->
        <div class="px-4 py-3">
            <div class="d-flex ai-center">
                <i class="iconfont icon-news"></i>
                <strong class="text-blue fs-lg ml-3">相关资讯</strong>
            </div>
            <div class="pt-3 ">
                <router-link 
                tag="div"
                v-for="item in model.related" 
                :key ="item._id"
                :to="`/articles/${item._id}`"
                class="py-1"
                >
                {{item.title}}
                </router-link>
            </div>
        </div>
    </div>
</template>

<style lang='scss'>
.page-article {
    .icon-news {
    font-size: 1.6923rem;
    }
    .body{
        img {
        max-width: 100%;
        height: auto;
    }
    iframe {
        width: 100%;
        height: auto;
    }
}
}
</style>

<script>
export default {
    props: {
    id: { required: true }
    },
    data() {
        return {
            model:null
        }
    },
    methods: {
        async fetch() {
            const res = await this.$http.get(`articles/${this.id}`);
            this.model = res.data
            console.log(this.model)
        }
    },
    created() {
        this.fetch();
    },

}
</script>