<template>
	<form @submit.prevent="$emit('form-submitted')">
		<slot />
	</form>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
export default Vue.extend({
	props: {
		action: {
			required: true,
			type: String
		} as PropOptions<string>,

		method: {
			required: true,
			type: String,
			default: 'get',
			validator: value => {
				return ['get', 'post'].includes(value)
			}
		} as PropOptions<string>
	}
})
</script>
