<template>
	<v-list-item>
		<h2 
			class="item"
			:class="todoItemClass"
			@click="toggleItem"
			>
			{{ todoItem.title }}
		</h2>
		<v-list-item-action>
			<v-btn
				   dark
				   color="red"
				   text
				   @click="removeTodo"
				   :style="{ margin:'0px 10px' }"
				   >
				remove
			</v-btn>
		</v-list-item-action>
	</v-list-item>
</template>

<script lang="ts">
import Vue, { PropType } from "vue";
import { Todo } from "@/App.vue";
	
	export default Vue.extend({
		props:{
			todoItem:{
				type: Object as PropType<Todo>	// Question) PropType
			},
			index:{
				type: Number,
				required: true
			}
		},
		methods: {
			removeTodo() {
				return this.$emit("remove", this.index);
			},
			toggleItem() {
				return this.$emit("toggle", this.todoItem, this.index);
			}
		},
		computed: {
			todoItemClass(): string | null {
				return this.todoItem.done ? 'complete' : null
			}
		}
	});
</script>

<style scoped>
	.item:hover {
		cursor: pointer;
	}
	.complete {
		text-decoration: line-through;
		color: grey;
	}
</style>