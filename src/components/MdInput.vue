<template>
  <div :class="wrapperClass">
      <i v-if="icon" :class="iconClass"/>
      <input :is="tag" :id="id" :class="className" :type="type" :placeholder="placeholder" :disabled="disabled" @focus="focus" @blur="blur" @click="wave" :checked="checked" :value="value" @change="change">
      <label v-if="label" :class="labelClass" :for="id">{{label}}</label>
      <slot></slot>
    </input>
  </div>
</template>

<script>
import classNames from 'classnames';
import 'font-awesome/css/font-awesome.min.css';
import waves from '../mixins/waves';

export default {
  props: {
    tag: {
      type: String,
      default: "input"
    },
    type: {
      type: String,
      default: "text"
    },
    id: {
      type: String
    },
    label: {
      type: String
    },
    filled: {
      type: Boolean
    },
    icon: {
      type: String,
    },
    placeholder: {
      type: String
    },
    size: {
      type: String
    },
    disabled: {
      type: [String, Boolean]
    },
    checked: {
      type: Boolean
    },
    navInput: {
      type: Boolean,
      default: false
    },
    gap: {
      type: Boolean,
      default: false
    },
    waves: {
      type: Boolean,
      default: false
    },
    wavesFixed: {
      type: Boolean,
      default: false
    },
    value: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      className: classNames(
        'form-control',
        this.type === 'checkbox' ? this.gap ? false : 'form-check-input' : false,
        this.type === 'radio' ? 'form-check-input' : false,
        this.filled && 'filled-in',
        this.gap ? 'with-gap' : false
      ),
      wrapperClass: classNames(
        this.navInput ? '' : this.type === 'checkbox' || this.type === 'radio' ? 'form-check my-3' : 'md-form',
        this.size ? 'form-' + this.size : '',
        this.waves ? 'ripple-parent' : ''
      ),
      iconClass: classNames(
        'fa',
        this.icon ? 'fa-'+this.icon : '',
        'prefix'
      ),
      labelClass: classNames(
        this.placeholder ? 'active': '',
        this.disabled ? 'disabled' : '',
        this.type === 'checkbox' || this.type === 'radio' ? 'form-check-label mr-5' : false
      ),
      innerValue: this.value
    };
  },
  methods: {
    focus(e) {
      const label = e.path[0].nextElementSibling;
      if (label) {
        label.classList.add('active');
      }
      // styles for navbar input
      if (this.navInput) {
        this.$el.firstElementChild.style.borderColor = "transparent";
        this.$el.firstElementChild.style.boxShadow = "none";
      }
    },
    blur(e) {
      const label = e.path[0].nextElementSibling;
      if (label) {
        if (label.parentElement.childNodes[2].value == ''){
          label.classList.remove('active');
        }
      }
      // styles for navbar input
      if (this.navInput) {
        this.$el.firstElementChild.style.borderColor = "#fff";
      }
    },
    change(e) {
      this.innerValue = e.path[0].value;
    }
  },
  mixins: [waves]
};
</script>

<style scoped>

</style>
