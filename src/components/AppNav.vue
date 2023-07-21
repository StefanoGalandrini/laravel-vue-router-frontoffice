<script>
export default {};
</script>

<template>
  <nav class="d-flex align-items-center">
    <ul class="footer-links d-flex gap-4 justify-content-center pt-3">
      <li class="list-unstyled">
        <router-link :to="{ name: 'home' }">
          <button class="button">HOME</button>
        </router-link>
      </li>

      <li class="list-unstyled">
        <router-link :to="{ name: 'about' }">
          <button class="button">CHI SIAMO</button>
        </router-link>
      </li>

      <li class="list-unstyled">
        <router-link :to="{ name: 'drinks' }">
          <button class="button">COCKTAILS</button>
        </router-link>
      </li>

      <li class="list-unstyled">
        <router-link :to="{ name: 'contacts' }">
          <button class="button">CONTACTS</button>
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css?family=Oswald:500");

// nav {
//   width: 100%;
//   position: fixed;
//   top:50px;
//   text-align:center;
// }

nav a {
  font-weight: 500;
  text-transform: uppercase;
  text-decoration: none;
  color: #ffffff;
  margin: 0 15px;
  font-size: 16px;
  letter-spacing: 1px;
  position: relative;
  display: inline-block;
}

nav a:before {
  content: "";
  position: absolute;
  width: 100%;
  height: 3px;
  background: #16151b;
  top: 47%;
  animation: out 0.2s cubic-bezier(1, 0, 0.58, 0.97) 1 both;
}

nav a:hover:before {
  animation: in 0.2s cubic-bezier(1, 0, 0.58, 0.97) 1 both;
}

@keyframes in {
  0% {
    width: 0;
    left: 0;
    right: auto;
  }
  100% {
    left: 0;
    right: auto;
    width: 100%;
  }
}

@keyframes out {
  0% {
    width: 100%;
    left: auto;
    right: 0;
  }
  100% {
    width: 0;
    left: auto;
    right: 0;
  }
}

@keyframes show {
  0% {
    opacity: 0;
    transform: translateY(-10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@for $i from 1 through 5 {
  nav a:nth-child(#{$i}) {
    animation: show 0.2s #{$i * 0.1+1}s ease 1 both;
  }
}

//buttons
.button {
  position: relative;
  padding: 10px 22px;
  border-radius: 6px;
  border: none;
  color: #fff;
  cursor: pointer;
  background-color: #7d2ae8;
  transition: all 0.2s ease;
}

.button:active {
  transform: scale(0.96);
}

.button:before,
.button:after {
  position: absolute;
  content: "";
  width: 150%;
  left: 50%;
  height: 100%;
  transform: translateX(-50%);
  z-index: -1000;
  background-repeat: no-repeat;
}

.button:hover:before {
  top: -70%;
  background-image: radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, transparent 20%, #7d2ae8 20%, transparent 30%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, transparent 10%, #7d2ae8 15%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%);
  background-size: 10% 10%, 20% 20%, 15% 15%, 20% 20%, 18% 18%, 10% 10%, 15% 15%,
    10% 10%, 18% 18%;
  background-position: 50% 120%;
  animation: greentopBubbles 0.6s ease;
}

@keyframes greentopBubbles {
  0% {
    background-position: 5% 90%, 10% 90%, 10% 90%, 15% 90%, 25% 90%, 25% 90%,
      40% 90%, 55% 90%, 70% 90%;
  }

  50% {
    background-position: 0% 80%, 0% 20%, 10% 40%, 20% 0%, 30% 30%, 22% 50%,
      50% 50%, 65% 20%, 90% 30%;
  }

  100% {
    background-position: 0% 70%, 0% 10%, 10% 30%, 20% -10%, 30% 20%, 22% 40%,
      50% 40%, 65% 10%, 90% 20%;
    background-size: 0% 0%, 0% 0%, 0% 0%, 0% 0%, 0% 0%, 0% 0%;
  }
}

.button:hover::after {
  bottom: -70%;
  background-image: radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, transparent 10%, #7d2ae8 15%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%),
    radial-gradient(circle, #7d2ae8 20%, transparent 20%);
  background-size: 15% 15%, 20% 20%, 18% 18%, 20% 20%, 15% 15%, 20% 20%, 18% 18%;
  background-position: 50% 0%;
  animation: greenbottomBubbles 0.6s ease;
}

@keyframes greenbottomBubbles {
  0% {
    background-position: 10% -10%, 30% 10%, 55% -10%, 70% -10%, 85% -10%,
      70% -10%, 70% 0%;
  }

  50% {
    background-position: 0% 80%, 20% 80%, 45% 60%, 60% 100%, 75% 70%, 95% 60%,
      105% 0%;
  }

  100% {
    background-position: 0% 90%, 20% 90%, 45% 70%, 60% 110%, 75% 80%, 95% 70%,
      110% 10%;
    background-size: 0% 0%, 0% 0%, 0% 0%, 0% 0%, 0% 0%, 0% 0%;
  }
}
</style>
