<template>
	<div :class="[gridClasses]">
		<slot />
	</div>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
import { GridGap } from '~/validators/Grid'

export default Vue.extend({
	props: {
		gap: {
			required: false,
			type: String,
			default: 'default',
			validator: (value) => {
				return Object.keys(GridGap).includes(value)
			},
		} as PropOptions<keyof typeof GridGap>,

		scrollTitle: {
			required: false,
			type: String,
		} as PropOptions<string>,
	},

	computed: {
		gridClasses(): string {
			return `${GridGap[this.gap]}`
		},
	},
})
</script>
