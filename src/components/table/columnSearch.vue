<template>
    <div>
        <div @click="showSearch">{{titleName}}<i class="el-icon-caret-top"></i></div>
        <el-input v-if="searchShow" v-model="search"size="mini" placeholder="" @keyup.enter.native="searchTable(querykey)">
            <i slot="suffix" class="el-input__icon el-icon-search" @click="searchTable(querykey)"></i>
        </el-input>
    </div>
</template>

<script>
    export default {
        props:{
        titleName:{
             type: String, // 传递的值必须是一个对象
             required: true // 这个值必须被传递过来
        },
        querykey:{
            type: String, // 传递的值必须是一个对象
             required: true // 这个值必须被传递过来
        }
        },
        data() {
            return {
            search:null,
            searchShow:false
            }
        },
        methods:{
           showSearch(){
                this.searchShow=!this.searchShow
            },
            searchTable(data){
                console.log(data)
            }
        }
    }
</script>

<style lang="scss" scoped>
     .el-table th div{
      display: block
    }
    .el-input__icon{
        text-align: left
    }
</style>