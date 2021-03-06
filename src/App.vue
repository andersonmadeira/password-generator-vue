<template>
  <main>
    <div class="app-container">
      <h1>
        <span role="img" aria-label="Key Icon">🔑</span>
        &nbsp; Password Generator
      </h1>
      <h2>Length: {{ length }}</h2>
      <Slider :length="length" @change="changeLength" />
      <h2>Characters:</h2>
      <Checkbox
        label="Lowercase (a-z)"
        :checked="lowercase"
        @change="lowercase = $event"
      />
      <Checkbox label="Uppercase (A-Z)" @change="uppercase = $event" />
      <Checkbox label="Numbers (0-9)" @change="numbers = $event" />
      <Checkbox label="Symbols (*!@%_#)" @change="symbols = $event" />
      <h2>Options</h2>
      <Checkbox
        label="Animation"
        :checked="true"
        @change="animation = $event"
      />
      <button class="button" @click="generatePassword">Generate</button>
      <Result
        :displayText="shuffledPassword ? shuffledPassword : generatedPassword"
        :text="generatedPassword"
      />
    </div>
  </main>
</template>

<script>
import Slider from './components/Slider'
import Checkbox from './components/Checkbox'
import Result from './components/Result'

export default {
  name: 'App',
  components: {
    Slider,
    Checkbox,
    Result,
  },
  data() {
    return {
      min: 1,
      max: 255,
      length: 20,
      lowercase: false,
      uppercase: false,
      numbers: false,
      symbols: false,
      animation: true,
      generatedPassword: '',
      shuffledPassword: '',
      shuffleInterval: 0,
    }
  },
  methods: {
    changeLength(newLength) {
      this.length = newLength
    },
    generatePassword() {
      if (
        !this.lowercase &&
        !this.uppercase &&
        !this.numbers &&
        !this.symbols
      ) {
        alert('Please select at least one character set!')
        return
      }

      const options = {
        length: this.length,
        lowercase: this.lowercase,
        uppercase: this.uppercase,
        numbers: this.numbers,
        symbols: this.symbols,
      }

      this.generatedPassword = this.getRandomPassword(options)

      let charIndex = 0

      if (this.shuffleInterval) {
        clearInterval(this.shuffleInterval)
      }

      this.shuffleInterval = window.setInterval(() => {
        if (charIndex > this.generatedPassword.length) {
          window.clearInterval(this.shuffleInterval)
          this.shuffleInterval = 0
          return
        }

        const newSuffleValue = [...new Array(this.generatedPassword.length)]
          .map((empty, i) =>
            i < charIndex
              ? this.generatedPassword[i]
              : this.getRandomChar(options)
          )
          .join('')

        this.shuffledPassword = newSuffleValue

        charIndex++
      }, 30)
    },
    getAlphabet(options) {
      const internalAlphabet =
        (options.lowercase ? 'abcdefghijklmnopqrstuvwxyz' : '') +
        (options.uppercase ? 'ABCDEFGHIJKLMNOPQRSTUVWXYZ' : '') +
        (options.numbers ? '0123456789' : '') +
        (options.symbols ? '!@#$%&*()_`´{[^~]};:/?<>,.=-+' : '')
      return internalAlphabet
    },
    getRandomChar(options) {
      const alphabet = this.getAlphabet(options)
      return alphabet.charAt(Math.floor(Math.random() * alphabet.length))
    },
    getRandomPassword(options) {
      const alphabet = this.getAlphabet(options)
      let result = ''

      for (let i = 0; i < options.length; i++) {
        result += alphabet.charAt(Math.floor(Math.random() * alphabet.length))
      }

      return result
    },
    copyToClipboard() {
      const inputElem = document.createElement('input')
      inputElem.value = this.generatedPassword
      document.body.appendChild(inputElem)

      inputElem.focus()
      inputElem.select()

      document.execCommand('copy')

      document.body.removeChild(inputElem)
    },
  },
  watch: {
    animation(newValue) {
      if (!newValue) {
        if (this.shuffleInterval) {
          window.clearInterval(this.shuffleInterval)
          this.shuffleInterval = 0
          this.shuffledPassword = ''
        }
      }
    },
  },
}
</script>

<style>
/* Global Styles */

@import url('https://fonts.googleapis.com/css?family=Rubik&display=swap');

* {
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  padding: 0;
}

body {
  background-color: #f3f7f7;
  font-family: 'Rubik', sans-serif;
  color: #39424e;
  font-size: 14px;
}

.app-container {
  max-width: 550px;
  margin: 0 auto;
  padding: 0 20px 20px 20px;
}

/* Button */

.button {
  font-size: 1.2em;

  color: #fff;
  font-weight: 700;

  border: none;
  border-radius: 2px;
  height: 40px;
  padding-left: 20px;
  padding-right: 20px;
  display: inline-block;

  box-shadow: 0 6px 16px 0 rgba(67, 184, 201, 0.2);
  background: #27b98c;
  border-color: #27b98c;

  outline: none;
  cursor: pointer;

  transition: all 0.5s ease;
}

.button:hover {
  background: #2cd39f;
}

/* Card */

.card {
  font-size: 1.5em;
  font-family: monospace;
  background-color: #fff;
  box-shadow: rgba(184, 194, 215, 0.35) 0px 6px 9px 0px;
  border-radius: 8px;
  padding: 46px 32px 40px 32px;
  position: relative;
  margin-top: 20px;
  word-break: break-all;
  transition: box-shadow 0.4s ease-in-out 0s,
    background-color 0.4s ease-in-out 0s;
}
</style>
