<template>
	<label :for="name">
		{{ label }}
		<slot />
	</label>
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
	},
})
</script>
