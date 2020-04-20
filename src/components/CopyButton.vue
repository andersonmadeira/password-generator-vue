<template>
  <button class="copy-button" @click="copyToClipboard">
    <svg class="svg-icon copy-button__icon" viewBox="0 0 20 20">
      <path
        d="M17.391,2.406H7.266c-0.232,0-0.422,0.19-0.422,0.422v3.797H3.047c-0.232,0-0.422,0.19-0.422,0.422v10.125c0,0.232,0.19,0.422,0.422,0.422h10.125c0.231,0,0.422-0.189,0.422-0.422v-3.797h3.797c0.232,0,0.422-0.19,0.422-0.422V2.828C17.812,2.596,17.623,2.406,17.391,2.406 M12.749,16.75h-9.28V7.469h3.375v5.484c0,0.231,0.19,0.422,0.422,0.422h5.483V16.75zM16.969,12.531H7.688V3.25h9.281V12.531z"
      />
    </svg>
    <span class="copy-button__label">copy</span>
  </button>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      required: true,
    },
  },
  methods: {
    copyToClipboard() {
      const inputElem = document.createElement('input')
      inputElem.value = this.text
      document.body.appendChild(inputElem)

      inputElem.focus()
      inputElem.select()

      document.execCommand('copy')

      document.body.removeChild(inputElem)
    },
  },
}
</script>

<style scoped>
.copy-button {
  position: absolute;
  top: 8px;
  left: 8px;
  border: none;
  background: none;
  outline: none;
  cursor: pointer;
  font: 1em Rubik, sans-serif;
  text-transform: uppercase;
  color: #757575;
  padding: 3px 10px;
  opacity: 0.4;
  transition: all 0.5s ease;
}

.copy-button .copy-button__icon {
  margin-right: 0.4em;
}

.copy-button:hover {
  opacity: 0.7;
}

.svg-icon {
  width: 1em;
  height: 1em;
}

.svg-icon path,
.svg-icon polygon,
.svg-icon rect {
  fill: #4691f6;
}

.svg-icon circle {
  stroke: #4691f6;
  stroke-width: 1;
}
</style>
