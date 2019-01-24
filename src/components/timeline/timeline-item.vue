<template>
	<li class="vux-timeline-item">
		<div :class="[
      'vux-timeline-item-color', {
        'vux-timeline-item-head': true
      }]" :style="headStyle">
			<!-- <icon v-show="isOver && $parent.isShowIcon" type="success_no_circle" class="vux-timeline-item-checked"></icon> -->
			<icon v-show="isAllow && $parent.isShowIcon" type="success" class="vux-timeline-item-isallow"></icon>
			<icon v-show="isReject && $parent.isShowIcon" type="warn" class="vux-timeline-item-isreject"></icon>
			<icon v-show="isCurrent && $parent.isShowIcon" type="circle" class="vux-timeline-item-iscurrent"></icon>
		</div>
		<div class="vux-timeline-item-tail" :style="tailStyle"></div>
		<div class="vux-timeline-item-content">
			<slot></slot>
		</div>
	</li>
</template>

<script>
import Icon from '../icon'

export default {
  name: 'timeline-item',
  data () {
    return {
      isLast: true,
      isFirst: true,
      headStyle: { backgroundColor: this.$parent.color }
    }
  },
  props: {
    isAllow: {
      type: Boolean,
      default: false
    },
    isReject: {
      type: Boolean,
      default: false
    },
    isCurrent: {
      type: Boolean,
      default: false
    }
  },
  mounted () {
    this.$parent.setChildProps()
  },
  beforeDestroy () {
    // this will be null
    const $parent = this.$parent
    this.$nextTick(() => {
      $parent.setChildProps()
    })
  },
  components: {
    Icon
  },
  computed: {
    tailStyle () {
      return this.isLast ? { display: 'none', backgroundColor: this.$parent.color } : { display: 'block', backgroundColor: this.$parent.color }
    }
  }
}
</script>

