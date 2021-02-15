<template>
	<div :class="[gridSectionSpanClasses]">
		<slot />
	</div>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'

import {
	GridSectionSpans,
	MediumGridSectionSpans,
	LargeGridSectionSpans,
	ExtraLargeGridSectionSpans,
	ExtraExtraLargeGridSectionSpans,
} from '~/validators/GridSectionSpans'

export default Vue.extend({
	props: {
		spans: {
			required: true,
			type: <unknown>Array,
		} as PropOptions<
			[
				keyof typeof GridSectionSpans,
				keyof typeof MediumGridSectionSpans,
				keyof typeof LargeGridSectionSpans,
				keyof typeof ExtraLargeGridSectionSpans,
				keyof typeof ExtraExtraLargeGridSectionSpans
			]
		>,
	},

	computed: {
		gridSectionSpans(): string {
			return `${GridSectionSpans[this.spans[0]]}
				${MediumGridSectionSpans[this.spans[1]]}
				${LargeGridSectionSpans[this.spans[2]]}
				${ExtraLargeGridSectionSpans[this.spans[3]]}
				${ExtraExtraLargeGridSectionSpans[this.spans[4]]}`
		},

		gridSectionSpanClasses(): string {
			return `${this.gridSectionSpans}`
		},
	},
})
</script>
