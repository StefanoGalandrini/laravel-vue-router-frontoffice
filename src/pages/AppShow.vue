<script>
import axios from "axios";
export default {
  data() {
    return {
      drink: null,
    };
  },
  methods: {
    formatIngredients(drink) {
      const ingredients = [];
      for (let i = 1; i <= 8; i++) {
        const ingredient = drink["strIngredient" + i];
        if (ingredient) {
          ingredients.push(ingredient);
        }
      }
      return ingredients.join(", ");
    },

    formatMeasures(drink) {
      const measures = [];
      for (let i = 1; i <= 8; i++) {
        const measure = drink["strMeasure" + i];
        if (measure) {
          measures.push(measure);
        }
      }
      return measures.join(", ");
    },
  },
  created() {
    // richiesta axios per i dati del post
    axios
      .get("http://localhost:8000/api/drinks/" + this.$route.params.id)
      .then((response) => {
        if (response.data.success) {
          const drinkData = response.data.results;
          this.drink = {
            ...drinkData,
            strInstructionsIT:
              drinkData.strInstructionsIT || drinkData.strInstructions,
          };
        }
      });
  },
};
</script>

<template>
  <div id="container">
    <!-- Start	Product details -->
    <div class="product-details" v-if="drink">
      <!-- 	Product Name -->
      <h1>{{ drink.strDrink }}</h1>

      <!-- The most important information about the product -->
      <p class="information my-5">
        {{ drink.strInstructionsIT }}
      </p>

      <button>
        <span></span>
        <span></span>
        <span></span>
        <span></span>
        <router-link :to="{ name: 'drinks' }"
          >Torna alla lista dei Drinks</router-link
        >
      </button>
    </div>

    <!-- 	End	Product details   -->

    <!-- 	Start product image & Information -->

    <div class="product-image" v-if="drink">
      <img :src="drink.strDrinkThumb" :alt="drink.strDrink" />

      <!-- 	product Information-->
      <div class="info">
        <h2 class="my-4">Informazioni sul Drink</h2>
        <ul>
          <li><strong>Categoria: </strong>{{ drink.strCategory }}</li>
          <li><strong>Tipo: </strong>{{ drink.strAlcoholic }}</li>
          <li>
            <strong>
              <!-- <font-awesome-icon :icon="['fas', 'martini-glass']" />  -->
              Bicchiere da usare: </strong
            >{{ drink.strGlass }}
          </li>
          <li><strong>Ingredienti: </strong>{{ formatIngredients(drink) }}</li>
          <li><strong>Dosi: </strong>{{ formatMeasures(drink) }}</li>
          <li v-if="drink.strTags">
            <strong>Tags: </strong>{{ drink.strTags }}
          </li>
        </ul>
      </div>
    </div>
    <!--  End product image  -->
  </div>
</template>

<style lang="scss" scoped>
/* fonts  */
@import url("https://fonts.googleapis.com/css?family=Abel|Aguafina+Script|Artifika|Athiti|Condiment|Dosis|Droid+Serif|Farsan|Gurajada|Josefin+Sans|Lato|Lora|Merriweather|Noto+Serif|Open+Sans+Condensed:300|Playfair+Display|Rasa|Sahitya|Share+Tech|Text+Me+One|Titillium+Web");

a {
  text-decoration: none;
  color: #ae00af;
}

#container {
  box-shadow: 0 15px 30px 1px rgba(128, 128, 128, 0.31);
  background: rgba(11, 9, 9, 0.9);
  text-align: center;
  border-radius: 5px;
  overflow: hidden;
  margin: 2em auto;
  height: 500px;
  width: 1200px;
  margin-top: 10rem;
}

/* 	Product details  */
.product-details {
  position: relative;
  text-align: left;
  overflow: hidden;
  padding: 30px;
  height: 100%;
  float: left;
  width: 40%;
}

/* 	Product Name */
#container .product-details h1 {
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  display: inline-block;
  position: relative;
  font-size: 34px;
  font-weight: 700;
  color: rgb(135, 39, 213);
}

#container .product-details h1:before {
  position: absolute;
  content: "";
  left: -10%;
  top: 240px;
  transform: translate(25px, -15px);
  font-family: "Farsan", cursive;
  display: inline-block;
  background: rgb(135, 39, 213);
  border-radius: 5px;
  font-size: 18px;
  padding: 9px;
  color: #fff;
  margin: 0;
  animation: chan-sh 6s ease infinite;
}

@keyframes chan-sh {
  from {
    content: "Try It!";
  }
  to {
    content: "New";
  }
}

/* The most important information about the product */
#container .product-details > p {
  font-family: "Farsan", cursive;
  text-align: center;
  font-size: 20px;
  color: white;
}

/* product image  */
.product-image {
  transition: all 0.3s ease-out;
  display: inline-block;
  position: relative;
  overflow: hidden;
  height: 100%;
  float: right;
  width: 50%;
  display: inline-block;
}

#container img {
  width: 100%;
  height: 100%;
}

.info {
  background: rgba(27, 26, 26, 0.9);
  font-family: "Farsan", cursive;
  transition: all 0.3s ease-out;
  transform: translateX(-100%);
  position: absolute;
  line-height: 1.9;
  text-align: left;
  font-size: 120%;
  cursor: default;
  color: #fff;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
  padding: 25px;
}

.info h2 {
  text-align: center;
}
.product-image:hover .info {
  transform: translateX(0);
}

.info ul li {
  transition: 0.3s ease;
}

.product-image:hover img {
  transition: all 0.3s ease-out;
}
.product-image:hover img {
  transform: scale(1.2, 1.2);
}

// BOTTONE PER TORNARE ALLA LISTA DEI DRINKS

button {
  position: absolute;
  bottom: 10%;
  left: 22%;
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
</style>
