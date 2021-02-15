<template>
	<div class="spacer" :class="[spacerClasses]"></div>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
import { SpacerSize } from '~/validators/Spacer'

import { BreakpointDisplay } from '~/validators/Breakpoint'

export default Vue.extend({
	name: 'component--spacer',

	props: {
		size: {
			required: false,
			type: String,
			default: 'default',
			validator: (value) => {
				return Object.keys(SpacerSize).includes(value)
			},
		} as PropOptions<keyof typeof SpacerSize>,

		breakpointDisplay: {
			required: false,
			type: String,
			default: 'default',
		} as PropOptions<keyof typeof BreakpointDisplay>,
	},

	computed: {
		spacerClasses(): string {
			return `${SpacerSize[this.size]} ${
				BreakpointDisplay[this.breakpointDisplay]
			}`
		},
	},
})
</script>
