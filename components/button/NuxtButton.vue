<template>
	<component :is="component" :href="href" :type="type" @button-clicked="$emit('button-clicked')">
		<slot />
	</component>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'

import { ButtonType } from '~/validators/Button'

export default Vue.extend({
	props: {
		type: {
			required: false,
			type: String,
			default: 'default',
			validator: (value) => {
				return ['default', 'link', 'submit'].includes(value)
			},
		} as PropOptions<keyof typeof ButtonType>,

		href: {
			required: false,
			type: [String, Boolean],
			default: false,
		} as PropOptions<string | boolean>,
	},

	components: {
		ButtonDefault: () => import(/* webpackChunkName: "ButtonDefault" */ './ButtonDefault.vue'),
		ButtonLink: () => import(/* webpackChunkName: "ButtonLink" */ './ButtonLink.vue'),
	},

	computed: {
		component(): string {
			return ButtonType[this.type]
		},
	},
})
</script>
