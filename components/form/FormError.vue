<template>
	<span>{{ error }}</span>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
export default Vue.extend({
	props: {
		error: {
			required: false,
			type: String,
		} as PropOptions<string | undefined>,
	},
})
</script>
