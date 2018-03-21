<template lang="pug">
.form-input
    label.sr-only(:for="inputName") {{capitalizedInputName}}
    input(:id="inputName" :name="inputName" :placeholder="capitalizedInputName" v-model="inputValue" @keyup="changeHandler")
</template>

<script>
export default {
  props: ['inputName'],
  data() {
    return {
      inputValue: ''
    };
  },
  computed: {
    capitalizedInputName() {
      const [firstLetter, ...otherLetters] = this.inputName;
      return firstLetter.toUpperCase() + otherLetters.join('');
    }
  },
  methods: {
    changeHandler() {
      this.$emit('change', {
        input: this.inputName,
        inputValue: this.inputValue
      });
    }
  }
};
</script>

<style scoped>
.form-input {
  margin-bottom: 1em;
}
.form-input > * {
  display: block;
  margin: 0.5em 0;
}

input {
  border-radius: 2px;
  padding: 1em 0.75em 0.6875em;
  width: 100%;
  background-color: #fff;
  border: 1px solid #dfe0e6;
  color: #1c1c1f;
  font-size: 0.9375em;
  line-height: normal;
  margin: 0;
}
</style>
