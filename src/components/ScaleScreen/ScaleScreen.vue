<template>
    <div :style="computeStyle" class="scale-box">
        <slot></slot>
    </div>
</template>

<script>
  const debounce = (fn, delay) => {
    let timer
    return function () {
      clearTimeout(timer)
      timer = setTimeout(fn.bind(this, ...arguments), delay)
    }
  }

  export default {
    name: 'ScaleScreen',
    props: {
      width: {
        default: 1366,
        type: Number
      },
      height: {
        default: 768,
        type: Number
      }
    },
    data() {
      return {
        scale: 1
      }
    },
    computed: {
      computeStyle() {
        return {
          width: `${this.width}px`,
          height: `${this.height}px`,
          transform: `scale(${this.scale}) translate(-50%, -50%)`
        }
      }
    },
    mounted () {
      this.getScale()
      window.addEventListener('resize', debounce(this.getScale, 200))
    },
    methods: {
      getScale() {
        // eslint-disable-next-line no-console
        const w = window.innerWidth / this.width
        const h = window.innerHeight / this.height
        this.scale = w < h ? w : h
      }
    }
  }
</script>

<style scoped>
.scale-box {
    transform-origin: 0 0;
    position: fixed;
    top: 50%;
    left: 50%;
    background: #fff;
}
</style>
