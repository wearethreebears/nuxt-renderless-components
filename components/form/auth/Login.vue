<template>
	<FormWrapper @form-submitted="login" method="post" action="#">
		<FormGroup :error="errors.get('email')">
			<FormInput
				label="Email"
				name="email"
				name-prefix="login"
				type="email"
				:value.sync="email"
				@reset-field="errors.clear('email')"
			/>
		</FormGroup>

		<FormGroup :error="errors.get('password')" @keyup="errors.clear('password')">
			<FormInput
				label="Password"
				name="password"
				type="password"
				name-prefix="login"
				:value.sync="password"
				@reset-field="errors.clear('password')"
			/>
		</FormGroup>
		<!--<NuxtButton type="submit">Submit</NuxtButton>-->
	</FormWrapper>
</template>

<script lang="ts">
import Vue from 'vue'
import NuxtButton from '~/components/button/NuxtButton.vue'

import { HelperFormErrors } from '~/helpers/form/HelperFormErrors.ts'

export default Vue.extend({
	components: { NuxtButton },
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
