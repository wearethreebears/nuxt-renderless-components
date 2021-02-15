<template>
	<FormWrapper @form-submitted="register" method="post" action="#">
		<FormGroup :error="errors.get('first_name')">
			<FormInput
				label="First name"
				name="first_name"
				:value.sync="firstName"
				@reset-field="errors.clear('first_name')"
			/>
		</FormGroup>

		<FormGroup :error="errors.get('last_name')">
			<FormInput
				label="Last name"
				name="last_name"
				:value.sync="lastName"
				@reset-field="errors.clear('last_name')"
			/>
		</FormGroup>

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

		<FormGroup
			:error="errors.get('confirm_password')"
			@keyup="errors.clear('confirm_password')"
		>
			<FormInput
				label="Password"
				name="confirm_password"
				type="password"
				:value.sync="confirmPassword"
				@reset-field="errors.clear('confirm_password')"
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
			firstName: '' as string,
			lastName: '' as string,
			email: '' as string,
			password: '' as string,
			confirmPassword: '' as string,
			errors: new HelperFormErrors(),
		}
	},
	methods: {
		async register(): Promise<void> {
			return new Promise((resolve, reject) => {})
		},
	},
})
</script>
