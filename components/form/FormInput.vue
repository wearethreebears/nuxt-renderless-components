<template>
	<FormLabel :label="label" :name="name">
		<input
			:type="type"
			:name="name"
			:id="name"
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
	},
})
</script>
