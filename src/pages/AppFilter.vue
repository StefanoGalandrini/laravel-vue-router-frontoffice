<script>
export default {
	data() {
		return {
			drinkTypes: [
				{
					name: "All",
					value: 1,
				},
				{
					name: "Alcoholic",
					value: 2,
				},
				{
					name: "Non alcoholic",
					value: 3,
				},
			],
		};
	},

	// methods: {
	// 	updateFilter(event) {
	// 		this.$emit("changeType", event.target.value);
	// 	},
	// },
};
</script>

<template>
	<select
		class="form-select w-25"
		@change="$emit('changeType', parseInt($event.target.value))">
		<!-- <option selected disabled>Choose</option> -->
		<option
			class="option"
			v-for="dtype in drinkTypes"
			:key="dtype.value"
			:value="dtype.value">
			{{ dtype.name }}
		</option>
	</select>
</template>

<style lang="scss" scoped>
select {
	margin: 1.75rem 0;
	display: flex;
	align-items: center;
	font-size: 1.25rem;

	.option {
		font-size: 1rem;
	}
}
</style>
