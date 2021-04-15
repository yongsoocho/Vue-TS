<template>
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
</template>

<script lang="ts">
import Vue from "vue";
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

<style scoped>

</style>