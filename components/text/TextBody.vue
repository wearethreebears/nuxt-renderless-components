<template>
	<div :class="[fontClasses]" v-html="text" />
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'
import { FontStyle, FontSize, FontColor, FontMargin } from '~/validators/Font'

export default Vue.extend({
	props: {
		text: {
			required: true,
			type: String,
		} as PropOptions<string>,

		style: {
			required: false,
			type: String,
			default: 'default',
		} as PropOptions<keyof typeof FontStyle>,

		size: {
			required: false,
			type: String,
			default: 'default',
		} as PropOptions<keyof typeof FontSize>,

		color: {
			required: false,
			type: String,
			default: 'default',
			validator: (value) => {
				return Object.keys(FontColor).includes(value)
			},
		} as PropOptions<keyof typeof FontColor>,

		margin: {
			required: false,
			type: String,
			default: 'default',
			validator: (value) => {
				return Object.keys(FontMargin).includes(value)
			},
		} as PropOptions<keyof typeof FontMargin>,
	},

	computed: {
		fontClasses(): string {
			return `${FontStyle[this.style]} ${FontSize[this.size]} ${
				FontColor[this.color]
			} ${FontMargin[this.margin]}`
		},
	},
})
</script>
