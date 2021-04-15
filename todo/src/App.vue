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
					<TodoListItem 
								  v-for="(todoItem, index) in todoItems" 
								  :key="index"
								  :index="index"
								  :todoItem="todoItem"
								  @remove="removeTodoItem"
								  @toggle="toggleTodoItemComplete"
								  ></TodoListItem>
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
	fetch(): Todo[] {
		const todoItems = localStorage.getItem(STORAGE_KEY) || "[]";
		const result = JSON.parse(todoItems);
		return result;
	},
	save(value: Todo[]) {
		const parsed = JSON.stringify(value);
		localStorage.setItem(STORAGE_KEY, parsed);
	}
}

export interface Todo {
	title: string;
	done: boolean;
}
	
export default Vue.extend({
	components: {
		TodoInput,
		TodoListItem
	},
	data() {
		return {
			todoText: "",
			todoItems: [] as Todo[]	// In Vue.js type define when initailize
		}
	},
	methods: {
		updateTodoText(value: any) {
			this.todoText = value;
		},
		addTodoItem() {
			const todo: Todo = {
				title: this.todoText,
				done: false
			};
			this.todoItems.push(todo);
			storage.save(this.todoItems);
			// localStorage.setItem(value, value);
			return this.initTodoText();
		},
		initTodoText() {
			return this.todoText = "";
		},
		fetchTodoItems() {
			this.todoItems = storage.fetch().sort((a: Todo, b: Todo) => {
				if(a.title < b.title) { 
					return -1;
				}
				if(a.title > b.title) { 
					return 1 
				};
				return 0;
			});
		},
		removeTodoItem(index: number) {
			this.todoItems.splice(index, 1);
			return storage.save(this.todoItems);
		},
		toggleTodoItemComplete(todoItem: Todo, index: number) {
			this.todoItems.splice(index, 1, {
				...todoItem,
				done: !todoItem.done
			});
			return storage.save(this.todoItems);
		}
	},
	created() {
		return this.fetchTodoItems();
	}
});
</script>

<style scoped>


</style>