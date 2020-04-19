<template>
  <input
    class="slider"
    type="range"
    :min="min"
    :max="max"
    step="1"
    :value="length"
    @input="changeLength"
  />
</template>

<script>
export default {
  name: 'Slider',
  props: {
    min: {
      type: Number,
      default: 1,
    },
    max: {
      type: Number,
      default: 255,
    },
    length: {
      type: Number,
      default: 20,
    },
  },
  methods: {
    changeLength(event) {
      this.$emit('change', Number(event.target.value))
    },
  },
}
</script>

<style scoped>
.slider {
  -webkit-appearance: none;
  width: 100%;
  height: 8px;
  border-radius: 5px;
  background: #d3d3d3;
  outline: none;
  opacity: 0.7;
  -webkit-transition: 0.2s;
  transition: opacity 0.2s;
}

.slider:hover {
  opacity: 1;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
  border-width: 3px;
  border-color: #afafaf;
  border-style: solid;
  cursor: pointer;
  transition: border-width 200ms ease-in-out, border-color 200ms ease-in-out;
}

.slider::-webkit-slider-thumb:hover {
  border-width: 4px;
  border-color: #27b98c;
}

.slider::-moz-range-thumb {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
  border-width: 3px;
  border-color: #afafaf;
  border-style: solid;
  cursor: pointer;
  transition: border-width 200ms ease-in-out, border-color 200ms ease-in-out;
}

.slider::-moz-range-thumb:hover {
  border-width: 4px;
  border-color: #27b98c;
}
</style>
