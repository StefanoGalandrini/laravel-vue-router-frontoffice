<script>
import axios from "axios";
import AppFilter from "./AppFilter.vue";
import {store} from "../store";

export default {
	components: {
		AppFilter,
	},

	data() {
		return {
			drinkType: null,
			drinks: [],
			loader: true,
			nPages: 0,
			currentPage: 1,
			allDrinks: [],
			store,
			drinksPerPage: 6,
		};
	},

	methods: {
		manageChangeType(type) {
			if (type === 1) {
				this.drinkType = null;
			} else if (type === 2) {
				this.drinkType = "Alcoholic";
			} else {
				this.drinkType = "Non alcoholic";
			}
			this.filterAndPaginateDrinks();
		},

		getDrinks() {
			(this.loader = true),
				axios
					.get(this.store.fixedUrl + "api/drinks", {
						params: {
							// page: this.currentPage,
							// type: this.drinkType,
						},
					})
					.then((response) => {
						this.allDrinks = response.data.results;
						// this.nPages = response.data.results.last_page;
						this.loader = false;
						this.filterAndPaginateDrinks();
					})
					.catch((error) => {
						this.loader = false;
						console.error(error);
					});
		},

		filterAndPaginateDrinks() {
			if (this.allDrinks) {
				const filteredDrinks = this.drinkType
					? this.allDrinks.filter(
							(drink) => drink.strAlcoholic === this.drinkType,
					  )
					: this.allDrinks;

				this.nPages = Math.ceil(filteredDrinks.length / this.drinksPerPage);
				this.paginateDrinks(filteredDrinks);
			}
		},

		paginateDrinks(drinks) {
			const start = (this.currentPage - 1) * this.drinksPerPage;
			const end = start + this.drinksPerPage;
			this.drinks = drinks.slice(start, end);
		},

		changePage(page) {
			this.currentPage = page;
			this.filterAndPaginateDrinks();
		},
	},

	created() {
		this.getDrinks();
	},

	watch: {
		drinkType() {
			this.currentPage = 1; // reset the current page to 1 when the filter changes
			this.filterAndPaginateDrinks();
		},
	},
};
</script>

<template>
	<main>
		<div class="container mt-0">
			<h1 class="text-center mt-5 mb-0">I Nostri Cocktails</h1>
			<div class="mb-3 w-100 d-flex justify-content-center gap-5">
				<AppFilter @changeType="manageChangeType($event)" />
				<nav>
					<div class="pagination p6">
						<ul>
							<a
								href="#"
								v-for="page in nPages"
								:key="page"
								class="page-item"
								:class="{is_active: page == currentPage}"
								@click="changePage(page)"
								><li></li
							></a>
						</ul>
					</div>
				</nav>
			</div>

			<div v-if="!loader" class="row row-cols-3 g2">
				<div v-for="drink in drinks" :key="drink.id" class="col z-3">
					<router-link
						class="text-decoration-none"
						:to="{name: 'drinks.show', params: {id: drink.id}}">
						<div class="drink_card mb-4">
							<img
								class="h-100"
								:src="drink.strDrinkThumb"
								:alt="drink.strDrink" />
							<p class="fs-6">{{ drink.strDrink }}</p>
						</div>
					</router-link>
				</div>
			</div>
			<div v-else>
				<div class="loader">
					<div class="loader_cube loader_cube--color"></div>
					<div class="loader_cube loader_cube--glowing"></div>
				</div>
			</div>
		</div>
	</main>
</template>

<style lang="scss" scoped>
$primary-color: #da00ff;
$secondary-color: #e81cff;
$tertiary-color: #40c9ff;
$quaternary-color: #fc00ff;
$quinary-color: #00dbde;

.bg_bar {
	position: absolute;
	// height: rem;
	bottom: 8rem;
	left: 0;
	transform: rotate(90deg);
}

.bg_drink {
	position: absolute;
	right: 0;
	bottom: 20rem;
	transform: rotate(270deg);
}
.container {
	margin-top: 5rem;
	margin-bottom: 5rem;
	h1 {
		color: $primary-color;
	}
	.row {
		margin-left: 9%;
	}
	nav {
		display: flex;
		justify-content: center;
	}
}

.drink_card {
	position: relative;
	width: 219px;
	height: 292px;
	background-color: #000;
	display: flex;
	flex-direction: column;
	justify-content: end;
	padding: 7px;
	gap: 12px;
	border-radius: 8px;
	cursor: pointer;

	&::before {
		content: "";
		position: absolute;
		inset: 0;
		left: -5px;
		margin: auto;
		width: 210px;
		height: 292px;
		border-radius: 10px;
		background: linear-gradient(
			-45deg,
			$secondary-color 0%,
			$tertiary-color 100%
		);
		z-index: -10;
		pointer-events: none;
		transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
	}

	&::after {
		content: "";
		z-index: -1;
		position: absolute;
		inset: 0;
		background: linear-gradient(
			-45deg,
			$quaternary-color 0%,
			$quinary-color 100%
		);
		transform: translate3d(0, 0, 0) scale(0.95);
		filter: blur(20px);
	}

	.heading {
		font-size: 20px;
		text-transform: capitalize;
		font-weight: 700;
	}

	p:not(.heading) {
		font-size: 14px;
	}

	p:last-child {
		color: $secondary-color;
		font-weight: 600;
		margin-bottom: 0;
	}

	&:hover::after {
		filter: blur(30px);
	}

	&:hover::before {
		transform: rotate(-90deg) scaleX(1.34) scaleY(0.77);
	}
}

// loader
.loader {
	width: 150px;
	height: 150px;
	margin: 10rem auto;
	position: relative;
	display: flex;
	align-items: center;
	justify-content: center;

	.loader_cube {
		position: absolute;
		width: 100%;
		height: 100%;
		border-radius: 30px;

		&--glowing {
			z-index: 2;
			background-color: rgba(255, 255, 255, 0.2);
			border: 2px solid rgba(255, 255, 255, 0.3);
		}

		&--color {
			z-index: 1;
			filter: blur(2px);
			background: linear-gradient(135deg, #1afbf0, $primary-color);
			animation: loadtwo 2.5s ease-in-out infinite;
		}
	}
}
@keyframes loadtwo {
	50% {
		transform: rotate(-80deg);
	}
}

// paginator

.pagination {
	padding: 30px 0;
}

.pagination ul {
	margin: 0;
	padding: 0;
	list-style-type: none;
}

.pagination a {
	display: inline-block;
	padding: 10px 18px;
	color: #222;
}

.p6 a {
	width: 30px;
	height: 30px;
	border-radius: 100%;
	padding: 0;
	margin: auto 5px;
	text-align: center;
	position: relative;
	background-color: $primary-color;
}

.p6 .is_active {
	background-color: $tertiary-color;
}
</style>
