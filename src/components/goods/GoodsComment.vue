<template>
    <cmtbox :id="$route.params.id"></cmtbox>
</template>
<script>
    import cmtbox from '../subcomponents/comments.vue'

    export default {
        components: {
            cmtbox
        }
    }
</script>
<style lang="scss" scoped>

</style>
