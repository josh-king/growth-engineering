<template>
        <div class="container">
  <section v-if="errored">
        <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
  </section>
  <section v-else>
      <div v-if="loading">Loading...</div>
      <div v-else>
          <div class="columns is-desktop is-multiline is-centered">
            <div v-for="items in info" :key="items.id">
              <div class="column">
                <div class="card">
                  <div class="card-image">
                    <div class="video-container">
                      <iframe width="100%" height="460" src="//youtube.com/embed/-vH2eZAM30s" frameborder="0" allowfullscreen></iframe>
                    </div>
                  </div>
                  <div class="card-content">
                    <div class="media">
                      <div class="media-left">
                        <figure class="image is-48x48">
                          <img :src="channelIcon" alt="Placeholder image">
                        </figure>
                      </div>
                      <div class="media-content">
                        <p class="title is-4">{{items.snippet.title}}</p>
                        <p class="subtitle is-6"><a :href="channelID">@{{items.snippet.channelTitle}}</a></p>
                      </div>
                    </div>

                    <div class="content">
                      {{items.snippet.description}}
                      <br>
                      <div v-if="items.status.privacyStatus == 'public'">
                        public
                      </div>
                      <div v-else-if="items.status.privacyStatus == 'unlisted'">
                        unlisted
                      </div>
                      <div v-else>
                        private
                      </div>
                      <time datetime="2016-1-1">{{items.snippet.publishedAt}}</time>
                    </div>
                  </div>
                </div>      
              </div>
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

Vue.use(VueAxios, axios)

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      info: [],
      loading: true,
      errored: false,
      title: '',
      channelIcon: "https://yt3.ggpht.com/-ejKSy49_U0Y/AAAAAAAAAAI/AAAAAAAAAAA/wnnvUIIoz1g/s288-mo-c-c0xffffffff-rj-k-no/photo.jpg",
      channelID: "https://www.youtube.com/channel/UCTI5S0PqpgB0DbYgcgRU6QQ"
    }
  },
  mounted () {
    axios
      .get('https://www.googleapis.com/youtube/v3/playlistItems?part=snippet%2CcontentDetails%2Cstatus&maxResults=5&playlistId=UUTI5S0PqpgB0DbYgcgRU6QQ&key=AIzaSyAZxPEU74h725HWmOiXNFRiujQKlzP6dmI')
      .then(response => {
        this.info = response.data.items
      })
      .catch(error => {
        // eslint-disable-next-line
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
