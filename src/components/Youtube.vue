<template>
  <div class="container">
    <section v-if="errored">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>
    <section v-else>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <div class="columns is-desktop is-multiline is-centered">
          <div v-for="item in items" :key="item.id">
            <VideoModule :channelIcon="icon"
                         :videoObject="item">
            </VideoModule>
          </div>  
        </div> 
      </div>
    </section>
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import VideoModule from './VideoModule.vue'

Vue.use(VueAxios, axios)

export default {
  name: 'Youtube',
  data () {
    return {
      items: [],
      loading: true,
      errored: false,
      title: '',
      icon: "https://yt3.ggpht.com/-ejKSy49_U0Y/AAAAAAAAAAI/AAAAAAAAAAA/wnnvUIIoz1g/s288-mo-c-c0xffffffff-rj-k-no/photo.jpg"
    }
  },
  mounted () {
    axios
      .get('https://www.googleapis.com/youtube/v3/playlistItems?part=snippet%2CcontentDetails%2Cstatus&maxResults=5&playlistId=UUTI5S0PqpgB0DbYgcgRU6QQ&key=AIzaSyAZxPEU74h725HWmOiXNFRiujQKlzP6dmI')
      .then(response => {
        this.items = response.data.items
      })
      .catch(error => {
        // eslint-disable-next-line
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  },
  components: {
    VideoModule
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
