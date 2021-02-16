<template>
	<div>
		<nav tabindex="0" ref="tabNavigation">
			<ul>
				<li v-for="(tab, index) in tabs" :key="tab.key">
					<button
						@click="onButtonClick(tab.key)"
						@keydown.tab.exact.prevent="onButtonTabDown($event)"
						@keydown.left.exact.prevent="onButtonArrowLeftDown($event)"
						@keydown.right.exact.prevent="onButtonArrowRightDown($event)"
						@keydown.shift.tab.exact="onButtonShiftTabDown"
						:data-index="index"
						ref="key"
						role="tab"
					>
						{{ tab.title }}
					</button>
				</li>
			</ul>
		</nav>
		<div>
			<template v-for="(tab, index) in tabs">
				<div
					:key="tab.key"
					v-if="hiddenTabs == 'rendered' || (hiddenTabs == 'unrendered' && activeTab == tab.key)"
					v-show="activeTab == tab.key"
					:aria-hidden="activeTab == tab.key ? 'false' : 'true'"
					ref="content"
					tabindex="0"
					:data-index="index"
					role="tabpanel"
					@keydown.shift.tab.exact.self="onPanelKeyDown($event)"
				>
					<slot :name="`${tab.key}`" />
				</div>
			</template>
		</div>
	</div>
</template>

<script lang="ts">
import Vue, { PropOptions } from 'vue'

import { Tab } from '~/interfaces/Tab'

export default Vue.extend({
	props: {
		tabs: {
			required: true,
			type: Array,
		} as PropOptions<Tab[]>,

		hiddenTabs: {
			required: false,
			type: String,
			default: 'rendered',
			validator: (value) => {
				return ['rendered', 'unrendered'].includes(value)
			},
		} as PropOptions<string>,
	},

	data() {
		return {
			activeTab: this.tabs[0].key as string,
		}
	},

	methods: {
		onButtonClick(key: string) {
			console.log(this.$parent)
			return (this.activeTab = key)
		},

		onButtonTabDown(event: KeyboardEvent): void {
			let index = (event.target as HTMLElement).getAttribute('data-index') as any

			let content = (this.$refs.content as HTMLElement[])[index]
			return content.focus()
		},

		onButtonArrowLeftDown(event: KeyboardEvent): void {
			let index = (event.target as HTMLElement).getAttribute('data-index') as any

			if (index > 0) {
				let newIndex = parseInt(index) - 1,
					key = (this.$refs.key as HTMLElement[])[newIndex]
				return key.focus()
			}

			return
		},

		onButtonArrowRightDown(event: KeyboardEvent): void {
			let index = (event.target as HTMLElement).getAttribute('data-index') as any

			if (index < this.tabs.length) {
				let newIndex = parseInt(index) + 1,
					key = (this.$refs.key as HTMLElement[])[newIndex]
				return key.focus()
			}

			return
		},

		onButtonShiftTabDown(event: KeyboardEvent): void {
			return (this.$refs.tabNavigation as HTMLElement).focus()
		},

		onPanelKeyDown(event: KeyboardEvent): void {
			let index = (event.target as HTMLElement).getAttribute('data-index') as any
			if (event.shiftKey && event.key === 'Tab') {
				event.preventDefault()
				let key = (this.$refs.key as HTMLElement[])[index]
				return key.focus()
			}
		},
	},
})
</script>
