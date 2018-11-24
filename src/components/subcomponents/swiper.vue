<template>
    <div>
        <mt-swipe :auto="4000">
            <!-- 在组件中， 使用v-for 循环的话， 一定要使用 key -->
            <!-- 将来，谁使用此轮播图组件， 谁为我们传递 lunbotuList -->
            <!-- 此时，lunbotuList 应该是 父组件向子组件传值来设置 -->
            <mt-swipe-item v-for="item in lunbotuList" :key="item.url">
                <img :src="item.img" alt="" :class="{'full': isfull }">
            </mt-swipe-item>
        </mt-swipe>
    </div>

    <!-- 分析： 为什么 商品评论中的轮播图 那么丑 -->
    <!-- 1. 首页中的图片， 他的宽和高， 都是使用了 100% -->
    <!-- 2. 在 商品详情页中， 轮播图的图片， 如果也使用 宽 高 为100%， 图片显示不好看 -->
    <!-- 3. 商品详情页中的轮播图， 期望高度是 100%， 宽度是自适应 -->
    <!-- 4. 经过分析， 问题的原因： 首页中的轮播图 和详情页中的轮播图 ，不同的是 宽度是100%还是自适应 -->
    <!-- 5. 两者间，只有宽度方面有不同，在其他方面没有不同， 可以定义一个属性，让使用轮播图的调用者， 手动指定 是否为 100% 宽 -->
</template>
<script>
    export default {
        props: ["lunbotuList","isfull"],
    }
</script>
<style lang="scss" scoped>
      .mint-swipe {
        height: 200px;
        .mint-swipe-item {
            text-align: center;
            img{
                width: 100%;
                height: 100%;
            }
        }
    }
    .full {
        width: 100%;
    }
</style>
