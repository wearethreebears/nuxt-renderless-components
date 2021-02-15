<template>
	<div data-component="form-group" class="">
		<slot />
		<FormError v-if="error" :error="error" />
	</div>
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
