<script>
import {Splide, SplideSlide} from "@splidejs/vue-splide";
import "@splidejs/splide/dist/css/splide.min.css";

export default {
	components: {
		Splide,
		SplideSlide,
	},

	data() {
		return {
			intervalId: null,

			carouselImages: [
				{
					src: "home-1.jpg",
					name: "Velvet Vesper",
					description: "A rich blend of blueberry and vanilla",
				},
				{
					src: "home-2.jpg",
					name: "Brasil Breeze",
					description: "$Refreshing cucumber with a hint of mint",
				},
				{
					src: "home-3.jpg",
					name: "Lavender Lust",
					description: "Sweet notes of strawberry and citrus",
				},
				{
					src: "home-4.jpg",
					name: "Tropical Tempest",
					description: "Warm honey flavors and spicy ginger",
				},
				{
					src: "home-5.jpg",
					name: "Midnight Martini",
					description: "Crisp apple with a blue curaçao twist",
				},
				{
					src: "home-6.jpg",
					name: "Cinnamon Celebration",
					description: "Tart pomegranate with a splash of lime",
				},
				{
					src: "home-7.jpg",
					name: "Ruby Radiance",
					description: "Minty freshness paired with tangy lime",
				},
				{
					src: "home-8.jpg",
					name: "Pomegranate Paradise",
					description: "A bold mix of fruit and liquor",
				},
			],
		};
	},

	methods: {
		getUrl(image) {
			return `/src/assets/img/${image.src}`;
		},

		nextImage() {
			this.$refs.splide.splide.go("+1");
		},

		prevImage() {
			this.$refs.splide.splide.go("-1");
		},

		stopAutoScroll() {
			if (this.intervalId !== null) {
				clearInterval(this.intervalId);
				this.intervalId = null;
			}
		},

		startAutoScroll() {
			if (this.intervalId === null) {
				this.intervalId = setInterval(this.nextImage, 2000);
			}
		},
	},

	mounted() {
		this.startAutoScroll();
	},

	beforeUnmount() {
		if (this.intervalId !== null) {
			clearInterval(this.intervalId);
			this.intervalId = null;
		}

		// Distruggere l'istanza Splide
		if (this.$refs.splide && this.$refs.splide.splide) {
			this.$refs.splide.splide.destroy();
		}
	},
};
</script>

<template>
	<div class="container home py-5 my-5">
		<h1 class="py-5">Welcome to MixTales!</h1>
		<div class="wrapper">
			<!-- Description Text -->
			<div class="text-container">
				<h2 class="title">Ti raccontiamo le nostre MixTales</h2>
				<p class="text">
					Un'esperienza unica e avvincente nel mondo dei cocktail, dove ogni
					sorso è una storia emozionante tra gusti, colori e profumi.
				</p>
			</div>

			<!-- Carousel -->
			<div class="carousel-container">
				<Splide
					ref="splide"
					class="carousel"
					:options="{
						type: 'loop',
						perPage: 3,
						perMove: 1,
						speed: 800,
						gap: '1rem',
						arrows: false,
						pagination: false,
						interval: 3000,
					}">
					<SplideSlide
						class="carousel-images"
						v-for="(image, index) in carouselImages"
						:key="index"
						@mouseover="stopAutoScroll"
						@mouseleave="startAutoScroll">
						<div>
							<img :src="getUrl(image)" :alt="image.name" />
							<p class="under-text name py-1">{{ image.name }}</p>
							<p class="under-text description py-2">{{ image.description }}</p>
						</div>
						<div class="image-text">
							<p class="type">Vieni a provarlo!</p>
						</div>
					</SplideSlide>
				</Splide>

				<div
					@mouseover="stopAutoScroll"
					@mouseleave="startAutoScroll"
					class="carousel-arrows">
					<i class="fa-solid fa-chevron-left" @click="prevImage"></i>
					<i class="fa-solid fa-chevron-right" @click="nextImage"></i>
					<!-- <font-awesome-icon icon="fa-solid fa-chevron-left" @click="prevImage" /> -->
					<!-- <font-awesome-icon
					icon="fa-solid fa-chevron-right"
					@click="nextImage" /> -->

        </div>
      </div>
    </div>
	<div class="container d-flex justify-content-center py-5">
		<button>
      	<router-link class="text-decoration-none" :to="{ name: 'about' }"
      	>Inizia il racconto</router-link
     	 >
    	</button>
	</div>
    
  </div>

</template>

<style lang="scss" scoped>
$mainColor: #55328b;
$textColor: #9685c2;




*,
*::after,
*::before {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

h1 {
	text-align: center;
	color: $mainColor;
	font-size: 3rem;
}

.wrapper {
	margin: 0 auto;
	display: grid;
	align-content: center;
	grid-template-columns: 2fr 5fr;
	grid-template-areas: "txt carousel";
	gap: 5rem;
	text-align: left;

	.text-container {
		grid-area: txt;
		align-self: center;

		.title {
			color: $mainColor;
			margin-bottom: 5rem;
			line-height: 4rem;
		}

		.text {
			color: $textColor;
			font-size: 1.2rem;
			font-style: italic;
			line-height: 2.5rem;
		}
	}
	.carousel-container {
		grid-area: carousel;
		position: relative;
		width: 100%;
		height: 100%;
		align-self: start;
		overflow: hidden;
	}
}

.under-text {
	height: 2.5rem;
	background-color: white;
	color: $mainColor;
}

.name {
	text-align: center;
	font-size: 1.5rem;
	font-weight: 700;
	line-height: 1.5rem;
	color: $mainColor;
}

.description {
	text-align: center;
	font-size: 1rem;
	line-height: 2rem;
	color: $textColor;
	border-bottom-left-radius: 15px;
	border-bottom-right-radius: 15px;
}

.splide__slide {
	max-width: 100%;
}

.carousel-images {
	width: 50%;
	height: 100%;
	display: flex;
	flex-wrap: nowrap;
	gap: 1rem;
	position: relative;

	.image-text {
		position: absolute;
		top: 40%;
		left: 50%;
		transform: translate(-50%, -50%);
		text-align: center;
		color: white;
		pointer-events: none;
		opacity: 0;
		transition: opacity 300ms ease-in-out;
	}

	&:hover .image-text {
		opacity: 1;
	}

	.type {
		margin: 0;
		padding: 0;
		white-space: nowrap;
		font-size: 0.8rem;
		line-height: 2rem;
		text-transform: uppercase;
		letter-spacing: 1px;
	}

	img {
		display: block;
		width: 100%;
		overflow: hidden;
		object-fit: cover;
		filter: brightness(0.9);
		margin-bottom: 1rem;
		transition: all 300ms;
		border-top-left-radius: 15px;
		border-top-right-radius: 15px;
		&:hover {
			filter: brightness(0.6);
		}
	}
}

.carousel-arrows {
	position: absolute;
	top: 50%;
	transform: translateY(calc(-50% - 2 * 2.2rem - 1rem));
	left: 0;
	right: 0;
	text-align: center;
}

.fa-chevron-left {
	line-height: 1rem;
	padding: 2.2rem 1rem;
	color: #523464;
	position: absolute;
	left: 0;
	font-size: 3em;
	&:hover {
		cursor: pointer;
	}
}

.fa-chevron-right {
	line-height: 1rem;
	padding: 2.2rem 1rem;
	color: #523464;
	position: absolute;
	right: 0;
	font-size: 3em;
	&:hover {
		cursor: pointer;
	}
}


// BOTTONE PER TORNARE ALLA LISTA DEI DRINKS

button {
  padding: 1em 1.8em;
  outline: none;
  border: 1px solid #303030;
  background: #212121;
  color: #ae00ff;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-size: 15px;
  overflow: hidden;
  transition: 0.2s;
  border-radius: 20px;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  box-shadow: 0 0 10px #ae00ff, 0 0 25px #001eff, 0 0 50px #ae00ff;
  transition-delay: 0.6s;
}

button span {
  position: absolute;
}

button span:nth-child(1) {
  top: 0;
  left: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #ae00ff);
}

button:hover span:nth-child(1) {
  left: 100%;
  transition: 0.7s;
}

button span:nth-child(3) {
  bottom: 0;
  right: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #001eff);
}
.start {
	width: 100%;
	display: flex;
	justify-content: center;
	padding: 1rem 2.5rem;

	.home-button {
		background-color: $mainColor;
		color: white;
		padding: 1rem 2rem;
		border-radius: 20rem;
		text-decoration: none;
		font-size: 1.3rem;
		margin: 0;
	}

}

button:hover span:nth-child(3) {
  right: 100%;
  transition: 0.7s;
  transition-delay: 0.35s;
}

button span:nth-child(2) {
  top: -100%;
  right: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(180deg, transparent, #ae00ff);
}

button:hover span:nth-child(2) {
  top: 100%;
  transition: 0.7s;
  transition-delay: 0.17s;
}

button span:nth-child(4) {
  bottom: -100%;
  left: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(360deg, transparent, #001eff);
}

button:hover span:nth-child(4) {
  bottom: 100%;
  transition: 0.7s;
  transition-delay: 0.52s;
}

button:active {
  background: #ae00af;
  background: linear-gradient(to top right, #ae00af, #001eff);
  color: #bfbfbf;
  box-shadow: 0 0 8px #ae00ff, 0 0 8px #001eff, 0 0 8px #ae00ff;
  transition: 0.1s;
}

button:active
  span:nth-child(1)
  span:nth-child(2)
  span:nth-child(2)
  span:nth-child(2) {
  transition: none;
  transition-delay: none;
}

// .start {
//   width: 100%;
//   display: flex;
//   justify-content: center;
//   padding: 1rem 2.5rem;

//   .home-button {
//     background-color: $mainColor;
//     color: white;
//     padding: 1rem 2rem;
//     border-radius: 20rem;
//     text-decoration: none;
//     font-size: 1.3rem;
//     margin: 0;
//   }
// }
</style>
