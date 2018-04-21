<template>
  <div :is="tag" :class="className">
    <img v-if="!isVideo" :src="src" :alt="alt" class="d-block w-100">
    <video v-if="isVideo" class="video-fluid d-block" :autoPlay="auto" :loop="loop">
      <source :src="src" type="video/mp4" />
    </video>
    <slot></slot>
  </div>
</template>

<script>
import classNames from 'classnames';

export default {
  props: {
    tag: {
      type: String,
      default: "div"
    },
    src: {
      type: String
    },
    alt: {
      type: String
    },
    loop: {
      type: Boolean
    },
    auto: {
      type: Boolean
    },
    full: {
      type: Boolean
    }
  },
  computed: {
    isVideo() {
      let videoFormats = ['webm', 'ogg', 'mp4'];
      const check = (formats, string) =>  {
        return formats.some(function(format){
          return string.endsWith(format);
        });
      };
      return check(videoFormats, this.src);
    }
  },
  data() {
    return {
      className: classNames(
        'carousel-item',
        this.full && 'full'
      ),
    };
  }
};
</script>

<style scoped>

</style>
