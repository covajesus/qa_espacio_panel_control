<template>
  <div>
    <div class="flex items-center justify-center h-screen">
      <div class="w-3/4 h-3/4">
        <audio controls>
          <source :src="`${post.audio_src}`" type="audio/mp3">
          Your browser does not support the audio element.
        </audio>
        <hr>
        {{ post.src_description }}2
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AudioDataComponent',
  props: {
    post: {
      type: Object,
      required: true
    }
  }
}
</script>
