<template>
	<div :class="[gridSectionClasses]">
		<slot />
	</div>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'

import {
	GridSectionStarts,
	MediumGridSectionStarts,
	LargeGridSectionStarts,
	ExtraLargeGridSectionStarts,
	ExtraExtraLargeGridSectionStarts,
	GridSectionEnds,
	MediumGridSectionEnds,
	LargeGridSectionEnds,
	ExtraLargeGridSectionEnds,
	ExtraExtraLargeGridSectionEnds,
} from '~/validators/GridSection'

export default Vue.extend({
	props: {
		starts: {
			required: true,
			type: <unknown>Array,
		} as PropOptions<
			[
				keyof typeof GridSectionStarts,
				keyof typeof MediumGridSectionStarts,
				keyof typeof LargeGridSectionStarts,
				keyof typeof ExtraLargeGridSectionStarts,
				keyof typeof ExtraExtraLargeGridSectionStarts
			]
		>,

		ends: {
			required: true,
			type: <unknown>Array,
		} as PropOptions<
			[
				keyof typeof GridSectionEnds,
				keyof typeof MediumGridSectionEnds,
				keyof typeof LargeGridSectionEnds,
				keyof typeof ExtraLargeGridSectionEnds,
				keyof typeof ExtraExtraLargeGridSectionEnds
			]
		>,
	},

	computed: {
		gridSectionStarts(): string {
			return `${GridSectionStarts[this.starts[0]]}
				${MediumGridSectionStarts[this.starts[1]]}
				${LargeGridSectionStarts[this.starts[2]]}
				${ExtraLargeGridSectionStarts[this.starts[3]]}
				${ExtraExtraLargeGridSectionStarts[this.starts[4]]}`
		},

		gridSectionEnds(): string {
			return `${GridSectionEnds[this.ends[0]]}
				${MediumGridSectionEnds[this.ends[1]]}
				${LargeGridSectionEnds[this.ends[2]]}
				${ExtraLargeGridSectionEnds[this.ends[3]]}
				${ExtraExtraLargeGridSectionEnds[this.ends[4]]}`
		},

		gridSectionClasses(): string {
			return `${this.gridSectionStarts} ${this.gridSectionEnds}`
		},
	},
})
</script>
