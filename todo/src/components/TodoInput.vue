<template>
  <div>
    <h1>To do list with TypeScript</h1>
    <v-container :style="{ display: 'flex', alignItems: 'center' }">
      <v-text-field
        color="blue"
        label="Today's todo"
        hide-details
        counter
        dense
        clearable
        :value="item"
        :style="{ width: '300px' }"
        @input="handleInput"
      />
      <v-btn
        dark
        color="blue"
        text
        @click="addTodo"
        :style="{ margin: '0px 5px' }"
      >
        ADD</v-btn
      >
    </v-container>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    item: {
      type: String,
      required: true,
    },
  },
  methods: {
    addTodo() {
      this.$emit("add");
    },
    handleInput(value: string) {
		if(value){
			return this.$emit("input", value);
		}
    },
  },
  data() {
    return {
      todoInput: [],
    };
  },
});
</script>

<style scoped></style>
