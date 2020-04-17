<template>
    <div class="page-hero" v-if="model">
    <!-- 开始顶部 -->
        <!-- ①黑顶 -->
        <div class="topbar bg-black d-flex py-2 px-3 ai-center text-white">
            <img src="../assets/logo.png" height="30" class="">
            <div class=" px-2 flex-1">
                <span>王者荣耀</span>
                <span class="ml-3">攻略站</span>
            </div>
            <router-link to="/" tag="div">更多英雄</router-link>
        </div>
        <!-- ② 图片背景栏 -->
        <div class="top" :style="{'background-image': `url(${model.banner})`}">
            <div class="text-white flex-column d-flex  info h-100 jc-end p-3" >
                <div class="fs-sm">{{model.title}}</div>
                <h2 class="my-2">{{model.name}}</h2>
                <!-- 数组的map方法 -->
                <div>{{model.categories.map(v => v.name).join('/')}}</div>
                <div class="d-flex jc-between">
                    <div class="d-flex ai-center scores" v-if="model.scores">
                        <span>难度</span>
                        <span class="badge bg-primary">{{model.scores.difficult}}</span>
                        <span>技能</span>
                        <span class="badge bg-blue-1">{{model.scores.skills}}</span>
                        <span>攻击</span>
                        <span class="badge bg-danger">{{model.scores.attack}}</span>
                        <span>生存</span>
                        <span class="badge bg-dark">{{model.scores.survive}}</span>
                    </div>
                    <div>
                        <router-link to="/" tag="span" class="flex-1 text-grey">
                            皮肤：7 &gt;
                        </router-link>
                    </div>
                </div>
            </div>
        </div>

        <!-- 正文部分 -->
        <div >
            <!-- 英雄初识 -->
            <div class="bg-white px-3">
                <div class="nav border-bottom d-flex jc-around pt-3 pb-2">
                    <div class="nav-item active">
                        <div>英雄初识</div>
                    </div>
                    <div class="nav-item">
                        <div>进阶攻略</div>
                    </div>
                </div>
            </div>

<!-- 写英雄初识标题栏 -->

            <swiper>
                <swiper-slide>
                    <div>
                        <!-- 技能组 -->
                        <div class="p-3 bg-white ">
                            <div class="d-flex jc-around">
                                <router-link tag="button" to="/" class="btn btn-lg flex-1">
                                    <i class="iconfont icon-shipin text-primary"></i>
                                    英雄介绍视频
                                </router-link>
                                <router-link tag="button" to="/" class="btn btn-lg flex-1 ml-2">
                                    <i class="iconfont icon-article text-primary"></i>
                                    一图识英雄
                                </router-link>
                            </div>

                            <!-- 四个技能 -->
                            <div>
                                <div class="d-flex jc-around skills">
                                    <img 
                                    :src="item.icon"
                                    class="icon"
                                    :class = "{active : currentSkillIndex ===i}"
                                    v-for="(item,i) in model.skills" :key="i"
                                    @click="currentSkillIndex =i"
                                    >
                                </div>
                                <div v-if="currentSkill">
                                    <div class="d-flex pt-4 pb-3 ai-center">
                                        <h2>{{currentSkill.name}}</h2>
                                        <span class="text-grey-1 ml-4 " >（冷却值： {{currentSkill.delay}}
                                            消耗： {{currentSkill.cost}} ）
                                        </span>
                                    </div>
                                    <div>
                                        {{currentSkill.description}}
                                    </div>
                                </div>
                            </div>
                        </div>


                        <!--  开始写出装推荐 这里要改写my-card-->
                        <my-card plain icon="superhero-" title="出装推荐">
                                <div class="fs-xl ">顺风出装</div>
                                <div class="d-flex jc-around text-center mt-3 skills">
                                    <div v-for="(item,i) in model.items1" :key="i" class=" ">
                                        <img :src="item.icon" class="icon">
                                        <div>{{item.name}}</div>
                                    </div>
                                </div>
                                <div class="border-bottom mb-3 mt-2"></div>

                                <div class="fs-xl ">逆风出装</div>
                                <div class="d-flex jc-around text-center mt-3 skills">
                                    <div v-for="(item,i) in model.items1" :key="i" class=" ">
                                        <img :src="item.icon" class="icon">
                                        <div>{{item.name}}</div>
                                    </div>
                                </div>    
                        </my-card>
                        
                        <my-card plain icon="superhero-" title="使用技巧">
                            <div>
                                {{model.usageTips}}
                            </div>
                        </my-card>

                        <my-card plain icon="superhero-" title="对抗技巧">
                            <div>
                                {{model.battleTips}}
                            </div>
                        </my-card>

                        <my-card plain icon="superhero-" title="团战技巧">
                            <div>
                                {{model.teamTips}}
                            </div>
                        </my-card>

                        <my-card plain icon="superhero-" title="英雄关系">
                            <div>
                                <div class="fs-xl">最佳搭档</div>
                                <div v-for="(item,i) in model.partners" :key="i" class="d-flex pt-3">
                                    <img :src="item.hero.avatar" height="70" width="70">
                                    <p class="flex-1 m-0 ml-2">{{item.description}}</p>
                                </div>
                                <div class="border-bottom mt-3"></div>
                            </div>
                        </my-card>
                    </div>
                </swiper-slide>
            </swiper>
        </div>
    </div>
</template>

<style lang="scss">
@import '../assets/scss/_variables.scss';
.page-hero {

    .top {
        height: 50vw;
        background: no-repeat top center;
        background-size: auto 100%;
    }
    .info {
            background: linear-gradient(rgba(0, 0, 0, 0), rgba(0, 0, 0, 1));
            .scores {
                .badge {
                    margin: 0 0.25rem;
                    display: inline-block;
                    width: 1rem;
                    height: 1rem;
                    border-radius: 50%;
                    line-height: 0.9rem;
                    text-align: center;
                    border: 1px solid rgba(255, 255, 255, 0.2);

                }
            }
    }
    .skills {
    img.icon {
        width: 70px;
        height: 70px;
        border: 3px solid map-get($colors, 'white');
        &.active {
        border-color:map-get($colors, 'primary');
        }
        border-radius: 50%;
    }
    }
    .hero-items {
        img.icon{
            width: 45px;
            height: 45px;
            border-radius: 50%;
        }
    }
}
</style>

<script>
export default {
    props: {
        id: {required: true}
    },
    data() {
        return {
            model:null,
            currentSkillIndex : 0
        }
    },
    computed: {
        currentSkill(){
            return this.model.skills[this.currentSkillIndex]
        }
    },
    methods: {
        async fetch() {
            const res =await this.$http.get(`heroes/${this.id}`)
            this.model = res.data
            console.log(res.data)
            // 获取完数据 开始要写页面！
        }
    },
    created() {
        this.fetch()
    },
    
}
</script>