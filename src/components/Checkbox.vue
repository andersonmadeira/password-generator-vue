<template>
  <div class="input-group">
    <label class="checkbox">
      {{ label }}
      <input type="checkbox" :checked="checked" @change="changeValue" />
      <span class="checkbox__checkmark"></span>
    </label>
  </div>
</template>

<script>
export default {
  props: {
    checked: {
      type: Boolean,
      default: false,
    },
    label: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      checkValue: false,
    }
  },
  created() {
    this.checkValue = this.checked
  },
  methods: {
    changeValue() {
      this.checkValue = !this.checkValue
      this.$emit('change', this.checkValue)
    },
  },
}
</script>

<style scoped>
/* Checkbox */

.checkbox {
  display: inline-block;
  position: relative;
  padding-left: 30px;
  margin-bottom: 12px;
  cursor: pointer;
  user-select: none;
  font-size: 1.2em;
}

.checkbox .checkbox__checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 3px 10px 0 rgba(0, 0, 0, 0.1);
  transition: all 0.5s ease;
}

.checkbox .checkbox__checkmark:after {
  content: '';
  position: absolute;
  display: none;
  left: 6px;
  top: 2px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  transform: rotate(45deg);
}

.checkbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkbox:hover input ~ .checkbox__checkmark {
  background-color: #f8fbfc;
}

.checkbox input:checked ~ .checkbox__checkmark {
  background-color: #27b98c;
}

.checkbox input:checked ~ .checkbox__checkmark:hover {
  background-color: #2cd39f;
}

.checkbox input:checked ~ .checkbox__checkmark:after {
  display: block;
}
</style>
