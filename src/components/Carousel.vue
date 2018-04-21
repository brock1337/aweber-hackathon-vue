<template>
  <div :is="tag" :class="className"><slot></slot></div>
</template>

<script>
import classNames from 'classnames';

export default {
  props: {
    tag: {
      type: String,
      default: "div"
    },
    interval: {
      type: Number,
      default: 10000
    },
    full: {
      type: Boolean,
      default: false
    },
    half: {
      type: Boolean,
      default: false
    },
    fade: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      className: classNames(
        'carousel',
        this.half && 'half',
        this.full && 'full',
        this.fade && 'carousel-fade'
      ),
      render: 0
    };
  },
  created() {
    if (this.render == 0) {
      this.$parent.$emit('defineInterval', {'newInterval': this.interval});
      this.render++;
    }
  }
};
</script>

<style scoped>

.full, .full carousel-item{
  height: 100% !important;
}

.half {
  height: 50%;
}
</style>
