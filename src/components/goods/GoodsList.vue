<template>
    <div class="goods-list">
        <!-- 在网页中， 有两种跳转方式 -->
        <!-- 方式1： 使用 a标签的形式 叫做 标签跳转 -->
        <!-- 方式2： 使用 window.location.href  的形式， 叫做 编程式导航 -->


        <!-- <router-link class="goods-item" v-for="item in goodslist" :key="item.id" tag="div" 
        :to="'/home/goodsinfo/'+ item.id">
            <img :src="item.img_url " alt="">
            <h1 class="title">{{ item.title }}</h1>
            <div class="info">
                <p class="price">
                    <span class="now">￥{{ item.sell_price }}</span>
                    <span class="old">￥{{ item.market_price }}</span>
                </p>
                <p class="sell">
                    <span>热卖中</span>
                    <span>剩{{ item.stock_quantity }}件</span>
                </p>
            </div>
        </router-link> -->

        <div class="goods-item" v-for="item in goodslist" :key="item.id" @click="goDetail(item.id)">
            <img :src="item.img_url " alt="">
            <h1 class="title">{{ item.title }}</h1>
            <div class="info">
                <p class="price">
                    <span class="now">￥{{ item.sell_price }}</span>
                    <span class="old">￥{{ item.market_price }}</span>
                </p>
                <p class="sell">
                    <span>热卖中</span>
                    <span>剩{{ item.stock_quantity }}件</span>
                </p>
            </div>
        </div>
        <mt-button type="danger" size="large" @tap="getMore"> 加载更多</mt-button>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                pageindex: 1, //分页的页数
                goodslist: []  //存放商品列表的数组
            }
        },
        created() {
            this.getGoodsList(); 
        },
        methods: {
            getGoodsList() {
                this.$http.get("api/getgoods?pageindex="+ this.pageindex).then( result => {
                    if(result.body.status === 0){
                        //this.goodslist = result.body.message;
                        this.goodslist = this.goodslist.concat(result.body.message);
                    }
                }) 
            },
            getMore() {
                this.pageindex++;
                this.getGoodsList();
            },
            goDetail(id) {
                    //使用 js 的形式进行路由导航

                    //注意： 区分 this.$route 和 this.$router 这两个对象
                    // this.$route:  是路由 【参数对象】，所有路由中的参数， params, query 都属于它
                    // this.$router: 是一个路由 【导航对象】， 用它 可以方便的使用js代码， 实现路由的前进、后退、跳转到新的 URL 地址
                  // console.log(this);
                   //1.最简单的
                   //this.router.push("home/goodsinfo/" + id);
                   //2. 传递对象
                  //this.$router.push({ path: "home/goodsinfo/" + id });
                   //3. 传递命名的路由
                this.$router.push({ name: 'goodsinfo', params: { id }});
            }
        },
       
    }
</script>
<style lang="scss" scoped>
.goods-list {
    display: flex;
    flex-wrap: wrap;
    padding: 7px;
    justify-content: space-between;
    .goods-item {
        width: 49%;
        border: 1px solid #ccc;
        box-shadow: 0 0 8px #ccc;
        margin: 4px 0;
        padding: 2px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        min-height: 293px;

        img{
            width: 100%;
            height: 200px;
        }
        .title {
            font-size: 14px;
        }
        .info{
            background-color: #eee;
            p{
                margin: 0;
                padding: 5px;
            }
            .price {
                .now {
                    color: red;
                    font-size: 16px;
                    font-weight: blod;
                }
                .old {
                    text-decoration: line-through;
                    font-size: 12px;
                    margin-left: 10px;
                }
            }
            .sell {
                display: flex;
                justify-content: space-between;
                font-size: 13px;
            }
        }


    }
}
</style>
