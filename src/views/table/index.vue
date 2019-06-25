<template>
  <div class="app-container">
    <el-table
      v-loading="listLoading"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row
    >
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column prop="id" align="center" label="ID" width="120">
        <template slot="header" slot-scope="scope">
          <columnSearch :titleName='columnName.id.name' :querykey="columnName.id.querykey"></columnSearch>
        </template> 
        <template slot-scope="scope">
          {{ scope.$index }}
        </template>
      </el-table-column>
      <el-table-column prop="title" label="Title">
        <template slot="header" slot-scope="scope">
          <columnSearch :titleName='columnName.title.name' :querykey='columnName.title.querykey'></columnSearch>
        </template> 
        <template slot-scope="scope">
          {{ scope.row.title }}
        </template>
      </el-table-column>
      <el-table-column prop="author" label="Author" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column prop="pageviews" label="Pageviews" width="110" align="center">
        <template slot-scope="scope">
          {{ scope.row.pageviews }}
        </template>
      </el-table-column>
      <el-table-column prop="status" class-name="status-col" label="Status" width="110" align="center" :filters='tableStatus' :filter-method="filterHandler">
        <template slot-scope="scope">
          <el-tag :type="scope.row.status | statusFilter">{{ scope.row.status }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column prop="display_time" align="center" label="Display_time" width="200">
        <template slot-scope="scope">
          <i class="el-icon-time" />
          <span>{{ scope.row.display_time }}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { getList } from '@/api/table'
import columnSearch from '@/components/table/columnSearch'
export default {
  components:{
    columnSearch
  },
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      list: null,
      listLoading: true,
      tableStatus:[
        {text: 'published', value:'published'},
        {text: 'draft', value: 'draft'},
        {text: 'deleted', value: 'deleted'}
      ],
      columnName:{
        id:{name:'ID号',
            querykey:'id'},
        title:{name:'标题',
              querykey:'title'}
      }
    }
   },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      this.listLoading = true
      getList().then(response => {
        this.list = response.data.items
        this.listLoading = false
      })
    },
    filterHandler(value, row, column){
      const property = column['property'];
      /**表格的每一列的props最好和返回来的数据的字段名称 */
      return row[property] === value;
    }
  }
}
</script>
<style lang="scss" scoped>
 
</style>
