<template>
    <div class="goodsdesc-container">
        <h3>{{ info.title }}</h3>
        <hr>
        <div class="content" v-html=" info.content">

        </div>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                info: []
            }
        },
        mounted() {
            this.getGoodsInfo();
        },
        methods: {
            getGoodsInfo() {
                this.$http.get("api/goods/getdesc/" + this.$route.params.id).then( result => {
                    if( result.body.status === 0 ){
                        this.info = result.body.message[0];
                    }
                })
            }
        }
    }
</script>
<style lang="scss">
    .goodsdesc-container {
        h3 {
            font-size: 16px;
            color: #226aff;
            text-align: center;
            margin: 15px 0;
        }
        .content {
            padding: 4px;
            img {
                width: 100%;
            }
        }
    }
</style>
