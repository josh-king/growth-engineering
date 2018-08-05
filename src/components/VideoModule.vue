<template>
    <div class="column">
        <div class="card">
            <div class="card-image">
                <div class="video-container">
                    <iframe width="100%" height="460" frameborder="0" :src="newURL" allowfullscreen></iframe>
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
                        <p class="title is-4">{{title}}</p>
                        <p class="subtitle is-6"><a :href="channel">@{{channelTitle}}</a></p>
                    </div>
                </div>
                    
                <div class="content">
                    {{description}}

                    <div class="video-properties">
                        <VideoProperties :privacy="videoPrivacy"></VideoProperties>
                    </div>                       
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import VideoProperties from './VideoProperties'

export default {
  name: 'VideoModule',
  props: {
    title: String,
    url: String,
    channelTitle: String,
    channelIcon: String,
    channelId: String,
    description: String
  },
  data () {
    return {
        newURL: "https://www.youtube.com/embed/" + this.url,
        channel: "https://www.youtube.com/channel/" + this.channelId,
        videoPrivacy: "public"
    }
  },
  components: {
      VideoProperties
  }
}
</script>

<style scope>
.video-properties {
    color: grey;
}
</style>
