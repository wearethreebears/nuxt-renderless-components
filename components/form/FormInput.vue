<template>
	<FormLabel :label="label" :name="id">
		<input
			:type="type"
			:name="name"
			:id="id"
			@keyup="$emit('update:value', $event.target.value)"
			@keydown="$emit('reset-field')"
		/>
	</FormLabel>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
export default Vue.extend({
	props: {
		name: {
			required: true,
			type: String,
		} as PropOptions<string>,

		label: {
			required: true,
			type: String,
		} as PropOptions<string>,

		type: {
			required: false,
			default: 'text',
			type: String,
			validator: (value) => {
				return ['text', 'email', 'password'].includes(value)
			},
		} as PropOptions<string>,

		value: {
			required: false,
			type: String,
		} as PropOptions<string>,

		namePrefix: {
			required: false,
			type: String,
		} as PropOptions<string>,
	},

	computed: {
		id(): string {
			return this.namePrefix
				? `${this.namePrefix}-${this.name}`
				: this.name
		},
	},
})
</script>
