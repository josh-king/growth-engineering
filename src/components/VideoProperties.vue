<template>
    <div v-if="privacy == 'public'">
      <i class="fas fa-globe-americas"></i> Public
    </div>
    <div v-else-if="privacy == 'unlisted'">
      <i class="fas fa-eye-slash"></i> Unlisted
    </div>
    <div v-else>
      <i class="fas fa-lock"></i> Private
    </div>
</template>

<script>
export default {
  name: 'VideoProperties',
  props: {
      privacy: String
  },
  data () {
    return {
    }
  }
}
</script>