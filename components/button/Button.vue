<template>
	<component
		:is="component"
		:href="href"
		:type="type"
		@button-clicked="$emit('button-clicked')"
	>
		<slot />
	</component>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
export default Vue.extend({
	props: {
		type: {
			required: false,
			type: String,
			validator: (value) => {
				return ['button', 'link', 'submit'].includes(value)
			},
		} as PropOptions<string>,

		href: {
			required: false,
			type: String || Boolean,
			default: false,
		} as PropOptions<string | boolean>,
	},

	components: {
		DefaultButton: () =>
			import(
				/* webpackChunkName: "DefaultButton" */ './DefaultButton.vue'
			),
		LinkButton: () =>
			import(/* webpackChunkName: "LinkButton" */ './LinkButton.vue'),
	},
})
</script>
