<template>
  <div class="matcher">
    <h2>Mariana's tags matcher</h2>
    <div class="inputs-container">
      <textarea v-model="input1"/>
      <textarea v-model="input2"/>
    </div>
    <div class="result">
      {{ matches }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Matcher',
  data() {
    return {
      input1: '',
      input2: '',
    };
  },
  computed: {
    matches() {
      if (!this.input1 || !this.input2) {
        return '';
      }

      const result = [];
      const inputArray1 = this.parseInput(this.input1);
      const inputArray2 = this.parseInput(this.input2);

      inputArray1.forEach((element) => {
        if (inputArray2.indexOf(element) !== -1) {
          result.push(element);
        }
      });

      return result.join(', ');
    }
  },
  methods: {
    parseInput(input) {
      return input.split(',').map((element) => {
        return element.trim().toLowerCase();
      });
    },
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

  .inputs-container textarea {
    flex-basis: 48%;
    height: 200px;
  }

  .result {
    margin-top: 2em;
    font-weight: bold;
  }
</style>
