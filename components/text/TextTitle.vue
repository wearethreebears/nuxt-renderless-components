<script lang="ts">
import Vue, { PropOptions } from 'vue'
import { FontStyle, FontSize, FontColor, FontMargin } from '~/validators/Font'

export default Vue.extend({
	render(createElement) {
		return createElement(
			`h${this.level}`, // tag name
			{
				attrs: {
					class: `
						${FontStyle[this.style]}
						${FontSize[this.size]}
						${FontColor[this.color]}
						${FontMargin[this.margin]}
                        ${this.customClass}
					`,
				},
			},
			this.$slots.default // array of children,
		)
	},

	props: {
		level: {
			required: true,
			type: Number,
			validator: (value) => {
				return value > 0 && value < 7
			},
		} as PropOptions<number>,

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

		customClass: {
			required: false,
			type: String,
			default: '',
		} as PropOptions<string>,

		margin: {
			required: false,
			type: String,
			default: 'default',
			validator: (value) => {
				return Object.keys(FontMargin).includes(value)
			},
		} as PropOptions<keyof typeof FontMargin>,
	},
})
</script>
