<template>
  <div id="wrapper">
    <h1>微信阅读</h1>
    <el-input v-model="input" placeholder="请输入内容">
      <el-button
        slot="append"
        icon="el-icon-search"
        @click="search"
      ></el-button>
    </el-input>
    <div style="margin-top: 50px">
      <el-table :data="searchList" border style="width: 100%">
        <el-table-column
          v-for="(item, key) in tableHeader"
          :key="key"
          :prop="item.prop"
          :label="item.label"
        >
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
import SystemInformation from './LandingPage/SystemInformation'

export default {
  name: 'landing-page',
  data() {
    return {
      input: '',
      searchList: [],
      tableHeader: [
        {
          prop: 'title',
          label: '书名',
        },
        {
          prop: 'author',
          label: '作者',
        },
        {
          prop: 'intro',
          label: '介绍',
        },
      ],
    }
  },
  methods: {
    async search() {
      console.log(this)
      let res = await this.$http.get(
        `https://weread.qq.com/web/search/global?keyword=${this.input}&maxIdx=0&fragmentSize=120&count=20`
      )
      res.data.books.map((key) => {
        this.searchList.push(key.bookInfo)
      })
      console.log(res, this.searchList)
    },
  },
}
</script>
<style>
</style>
