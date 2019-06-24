<template>
    <div>
        <div @click="showSearch">ID <i class="el-icon-caret-top"></i></div>
        <el-input v-if="searchShow" v-model="search"size="mini" placeholder="" suffix-icon="el-icon-search"/>
    </div>
</template>

<script>
    export default {
        data() {
            return {
            search:null,
            searchShow:false
            }
        },
        methods:{
           showSearch(){
                this.searchShow=!this.searchShow
            } 
        }
    }
</script>

<style lang="scss" scoped>

</style>