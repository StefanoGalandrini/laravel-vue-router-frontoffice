<script>
import axios from "axios";
export default {
  data() {
    return {
      drinks: [],
      currentPage: 1,
      nPages: 0,
      // firstPage: false,
      // lastPage: false,
      loader: true,
    };
  },
  methods: {
    getDrinks() {
      (this.loader = true),
        axios
          .get("http://localhost:8000/api/drinks", {
            params: {
              page: this.currentPage,
            },
          })
          .then((response) => {
            this.drinks = response.data.results.data;
            this.nPages = response.data.results.last_page;
            this.loader = false;
          });
    },
    changePage(page) {
      this.currentPage = page;
      // if (this.currentPage <= 1) {
      //   this.firstPage = !this.firstPage;
      // } else {
      //   this.firstPage = false;
      // }
      // if (this.currentPage >= this.nPages) {
      //   this.lastPage = !this.lastPage;
      // } else {
      //   this.lastPage = false;
      // }
    },
    // nextPage() {
    //   this.currentPage++;
    //   if (this.currentPage >= this.nPages) {
    //     this.lastPage = true;
    //   }
    //   this.firstPage = false;
    // },
    // previousPage() {
    //   this.currentPage--;
    //   if (this.currentPage <= 1) {
    //     this.firstPage = true;
    //   }
    //   this.lastPage = false;
    // },
  },
  created() {
    this.getDrinks();
  },
  watch: {
    currentPage() {
      this.getDrinks();
    },
  },
};
</script>

<template>
  <main>

    <div class="container">
      
      <h1 class="text-center mt-3">I Nostri Cocktails</h1>
      
      <div v-if="!loader" class="row row-cols-3 g-5 my-5">
        <div v-for="drink in drinks" :key="drink.id" class="col z-3">
          <router-link
            class="text-decoration-none"
            :to="{ name: 'drinks.show', params: { id: drink.id } }"
          >
            <div class="drink_card">
              <img
                class="h-100"
                :src="drink.strDrinkThumb"
                :alt="drink.strDrink"
              />
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
      
      <nav>
        <div class="pagination p6">
          <ul>
            <a
              href="#"
              v-for="page in nPages"
              :key="page"
              class="page-item"
              :class="{ is_active: page == currentPage }"
              @click="changePage(page)"
              ><li></li
            ></a>
          </ul>
        </div>
      </nav>

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

// ul.pagination {
//   --bs-pagination-border-color: black;
//   .page-item {
//     .page-link {
//       color: $secondary-color;

//       &:hover {
//         background-color: gray;
//         color: $secondary-color;
//         border-color: $secondary-color;
//       }
//     }

//     &.active {
//       .page-link {
//         background-color: gray;
//         border-color: $secondary-color;
//       }
//     }
//   }
// }
</style>
