<template>
  <div>

    <div class="music">
      <div v-for="(music,index) in musicList" class="music-item" @click="linkToMusic(music,index)">
        {{ music.title }}
        <aplayer v-if="currentIndex === index" autoplay
          :music="currentMusic"
        />
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import Aplayer from 'vue-aplayer'

  export default {
    data() {
      return {
        currentIndex:null,
        musicList: [],
        currentMusic:{}
      }
    },
    mounted () {
      this.getMusicList()
    },
    components: {
      Aplayer,
    },
    methods: {
      linkToMusic(music,index){
        this.currentMusic = music
        this.currentIndex = index
        // window.open(music.src)
      },
      getMusicList() {
        axios.get('https://www.kaier001.com/api/v1/music/list?pageIndex=1&pageSize=100&keywords=').then((res)=>{
          console.log('res',res.data.data);
          this.musicList = res.data.data.list || []
        })
      }
    },
  }
</script>

<style scoped>
.music-item{
  padding: 20px;
}
.music-item:hover{
  color:#3eaf7c;
  cursor: pointer;
}
</style>