<template>
<v-app>
	<v-row>
		<v-col cols="3"></v-col>
		<v-col 
			   cols="6"
			   :style="{ justifyContent:'center' }"
			   >
			<TodoInput 
					   :item="todoText" 
					   @input="updateTodoText"
					   @add="addTodoItem"
					   ></TodoInput>
			<div>
				<v-list>
					<TodoListItem></TodoListItem>
				</v-list>
			</div>
		</v-col>
		<v-col cols="3"></v-col>
	</v-row>
</v-app>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoListItem from "./components/TodoListItem.vue";

const STORAGE_KEY = 'vue-todo-items';
	
const storage = {
	fetch() {
		const todoItems: string = localStorage.getItem(STORAGE_KEY) || "[]";
		const result: any[] = JSON.parse(todoItems);
		return result;
	},
	save(value: any[]) {
		const parsed = JSON.stringify(value);
		localStorage.setItem(STORAGE_KEY, parsed);
	}
}
	
export default Vue.extend({
	components: {
		TodoInput,
		TodoListItem
	},
	data() {
		return {
			todoText: "",
			todoItems: []
		}
	},
	methods: {
		updateTodoText(value: any) {
			this.todoText = value;
		},
		addTodoItem() {
			const value = this.todoText;
			this.todoItems.push(value);
			storage.save(this.todoItems);
			// localStorage.setItem(value, value);
			return this.initTodoText();
		},
		initTodoText() {
			return this.todoText = "";
		},
		fetchTodoItems() {
			this.todoItems = storage.fetch();
		}
	},
	created() {
		return this.fetchTodoItems();
	}
});
</script>

<style scoped>


</style>