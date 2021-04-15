<template>
<<<<<<< HEAD
<v-app>
	<v-row>
		<v-col cols="3"></v-col>
		<v-col 
			   cols="6"
			   :style="{ justifyContent:'center' }"
			   >
			<TodoInput :item="todoText" @input="updateTodoText" @add="addTodoItem"></TodoInput>
		</v-col>
		<v-col cols="3"></v-col>
	</v-row>
</v-app>
=======
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
  </div>
>>>>>>> 617348f676f53cd0b71815a5664809fdd1f5fa40
</template>

<script lang="ts">
import Vue from "vue";
<<<<<<< HEAD
import TodoInput from "./components/TodoInput.vue";

export default Vue.extend({
	components: {
		TodoInput,	
	},
	data() {
		return {
			todoText: ""
		}
	},
	methods: {
		updateTodoText(value: any) {
			this.todoText = value;
		},
		addTodoItem() {
			const value = this.todoText
			localStorage.setItem(value, value);
			return this.initTodoText();
		},
		initTodoText() {
			return this.todoText = "";
		}
	}
});
</script>
=======
import HelloWorld from "./components/HelloWorld.vue";

export default Vue.extend({
  name: "App",
  components: {
    HelloWorld,
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
>>>>>>> 617348f676f53cd0b71815a5664809fdd1f5fa40
