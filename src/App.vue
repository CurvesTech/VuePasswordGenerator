<template>
  <div>
    <div id="output">
      <h1>Password Generator</h1>
      <p v-if="password">{{ password }}</p>
    </div>
    <div id="configWrapper">
      <div class="config-item">
        <h3>Password Case</h3>
        <div>
          <label for="uppercase">
            <input type="radio" name="case" v-model="config.passwordCase" id="uppercase" value="uppercase">
            Upper Case
          </label>
          <label for="lowercase">
            <input type="radio" name="case" v-model="config.passwordCase" id="lowercase" value="lowercase">
            Lower Case
          </label>
          <label for="mixedcase">
            <input type="radio" name="case" v-model="config.passwordCase" id="mixedcase" value="mixedcase">
            Mixed Case
          </label>
        </div>
      </div>

      <div class="config-item">
        <h3>Character Types</h3>
        <div>
          <label for="alpha_numeric">
            <input type="checkbox" name="char_types_alpha_numeric" v-model="config.alphaNumeric" id="alpha_numeric">
            Alpha Numeric
          </label>
          <label for="special_chars">
            <input type="checkbox" name="char_types_special_chars" v-model="config.specialChars" id="special_chars">
            Special Characters
          </label>
        </div>
      </div>

      <div class="config-item">
        <h3>Length</h3>
        <input id="numLength" type="number" v-model="config.length">
      </div>

      <button @click="generate()" id="btnGenerate">Generate</button>

    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        password: '',
        config: {
          passwordCase: 'uppercase',  // uppercase, lowercase, mixedcase,
          alphaNumeric: true,
          specialChars: false,
          length: 10
        }
      }
    },

    methods: {
      generate() {
        let pool = '';
        if(this.config.passwordCase == 'uppercase') {
          pool = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
        } else if(this.config.passwordCase == 'lowercase') {
          pool = 'abcdefghijklmnopqrstuvwxyz';
        } else {
          pool = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
        }

        if(this.config.alphaNumeric) {
          pool += '1234567890';
        }

        if(this.config.specialChars) {
          pool += '!@#$%^&*-=+/';
        }

        this.password = '';
        for(let i=0; i<this.config.length; i++) {
          const randomIndex = Math.floor( Math.random() * pool.length );
          this.password += pool.charAt(randomIndex);
        }
        
      }
    }
  }
</script>