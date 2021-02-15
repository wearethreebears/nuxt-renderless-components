<template>
	<button :type="type" @click="$emit('button-clicked')"><slot /></button>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
export default Vue.extend({
	props: {
		type: {
			required: true,
			type: String,
			validator: (value) => {
				return ['button', 'submit'].includes(value)
			},
		} as PropOptions<string>,
	},
})
</script>
