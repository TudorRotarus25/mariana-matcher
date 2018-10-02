<template>
  <div class="matcher">
    <h2>Mariana's tags matcher</h2>
    <div class="inputs-container">
      <div class="container">
        <div class="backdrop">
          <div class="highlights">
            <span
              v-for="(word, index) in wordsLeft"
              :key="index"
              :class="{ 'mark': matches.indexOf(word) !== -1 }"
            >
              {{ word }},
            </span>
          </div>
        </div>
        <textarea :value="wordsLeft.join(', ')" @input="changeWordsLeft"/>
      </div>
      <div class="container">
        <div class="backdrop">
          <div class="highlights">
            <span
                v-for="(word, index) in wordsRight"
                :key="index"
                :class="{ 'mark': matches.indexOf(word) !== -1 }"
            >
              {{ word }},
            </span>
          </div>
        </div>
        <textarea :value="wordsRight.join(', ')" @input="changeWordsRight"/>
      </div>
    </div>
    <div class="result">
      {{ matches.join(', ') }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Matcher',
  data() {
    return {
      wordsLeft: [],
      wordsRight: [],
    };
  },
  computed: {
    matches() {
      const result = [];

      this.wordsLeft.forEach((element) => {
        if (this.wordsRight.indexOf(element) !== -1) {
          result.push(element);
        }
      });

      return result;
    }
  },
  methods: {
    parseInput(input) {
      return input.split(/ or |,/).map((element) => {
        return element.trim().toLowerCase();
      });
    },
    changeWordsLeft(event) {
      this.wordsLeft = this.parseInput(event.target.value);
    },
    changeWordsRight(event) {
      this.wordsRight = this.parseInput(event.target.value);
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .matcher {
    max-width: 1200px;
    margin: auto;
  }

  .inputs-container {
    display: flex;
    justify-content: space-between;
  }

  .inputs-container .container {
    position: relative;
    flex-basis: 48%;
    height: 200px;
  }

  .inputs-container .container textarea {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    margin: 0;
    padding: 5px;
    border-radius: 0;
    width: calc(100% - 6px);
    color: #444; /* or whatever */
    background-color: transparent;
    font-size: 14px;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
  }

  .result {
    margin-top: 2em;
    font-weight: bold;
  }

  .backdrop {
    position: absolute;
    padding: 6px;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    overflow: auto;
    color: transparent;
    background-color: #fff;
    font-size: 14px;
    text-align: left;
  }

  .highlights .mark {
    color: transparent;
    background-color: #a0ff94; /* or whatever */
  }

</style>
