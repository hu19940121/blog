<template>
  <div>
    <span @click="download">
    {{ downUrl ? '点击下载' : 'loading.....' }}
    </span>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data() {
      return {
        downUrl:''
      }
    },
    mounted () {
      this.getUrl()
    },
    methods: {
      download() {
        window.open(this.downUrl)
      },
      getUrl() {
        axios.get('https://kaier001.com/api/v2/spider/lolskin').then((res)=>{
          this.downUrl = res.data.data || ''
        })
      }
    },
  }
</script>

<style scoped>
span{
  cursor: pointer;
}
</style>