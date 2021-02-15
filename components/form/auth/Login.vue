<template>
	<FormWrapper @form-submitted="login" method="post" action="#">
		<FormGroup :error="errors.get('email')">
			<FormInput
				label="Email"
				name="email"
				type="email"
				:value.sync="email"
				@reset-field="errors.clear('email')"
			/>
		</FormGroup>

		<FormGroup
			:error="errors.get('password')"
			@keyup="errors.clear('password')"
		>
			<FormInput
				label="Password"
				name="password"
				type="password"
				:value.sync="password"
				@reset-field="errors.clear('password')"
			/>
		</FormGroup>
		<button type="submit" class="bg-blue-500 text-white" value="">
			Submit
		</button>
	</FormWrapper>
</template>

<script lang="ts">
import Vue from 'vue'

import { HelperFormErrors } from '~/helpers/form/HelperFormErrors.ts'

export default Vue.extend({
	data() {
		return {
			email: '' as string,
			password: '' as string,
			errors: new HelperFormErrors(),
		}
	},
	methods: {
		async login(): Promise<void> {
			await this.$auth
				.loginWith('laravelSanctum', {
					data: {
						email: this.email,
						password: this.password,
					},
				})
				.then(() => {
					this.$router.push('/')
				})
				.catch(({ response }) => {
					this.errors.record(response.data.errors)
				})
		},
	},
})
</script>
