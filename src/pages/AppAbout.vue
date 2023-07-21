<script>
export default {};
</script>

<template>
  <div class="about py-5">
    <h1 style="font-style: italic; font-size: 4em" class="text-center py-3">
      Chi siamo...
    </h1>

    <div class="container d-flex">
      <i class="fa-solid fa-quote-left"></i>
      <h4 style="font-style: italic" class="text-center">
        Siamo un team di appassionati e esperti mixologist, con una passione
        sconfinata per la creazione di cocktail straordinari. Con anni di
        esperienza nel settore, siamo determinati a fornire i migliori cocktail
        che renderanno ogni occasione memorabile.
      </h4>
      <i class="fa-solid fa-quote-right"></i>
    </div>

    <div class="container py-5">
      <h2>La nostra filosofia...</h2>
      <div class="d-flex">
        <p class="fs-4">
          Al centro di tutto ciò che facciamo, c'è l'amore per gli ingredienti
          di alta qualità e l'attenzione per i dettagli. <br />
          I nostri cocktail sono realizzati con cura, utilizzando solo
          ingredienti freschi,<br />
          selezionati con attenzione per garantire un gusto superiore e
          un'esperienza gustativa indimenticabile.
        </p>
        <div class="philosophy mx-5">
          <div class="philosopy_content">
            <img
              style="height: 240px; border-radius: 20px; width: 250px;"
              src="../../public/drink.philosophy.jpg"
              alt=""
            />
          </div>
        </div>
      </div>
    </div>

    <div class="container menu py-5">
      <div class="text-center">
        <h2>Il nostro menu</h2>
        <i class="fa-solid fa-quote-left"></i>
        <p class="fs-4">
          Il nostro menu di cocktail è una fusione di classici intramontabili
          e creazioni innovative. Dai mojito rinfrescanti e dai negroni
          avvolgenti, fino alle nostre invenzioni esclusive, ogni drink è un
          viaggio sensoriale che vi porterà in luoghi lontani e spazierà tra
          le emozioni.
        </p>
        <i class="fa-solid fa-quote-right"></i>
      </div>
    </div>
    <div class="container py-3">
      <img
        style="
          width: 100%;
          box-shadow: rgba(151, 65, 252, 0.2) 0 35px 40px 20px;
          border-radius: 30px;
        "
        src="../../public/drink-menu.jpg"
        alt=""
      />
    </div>

    <div class="container menu py-5">
      <div class="text-center">
        <h2>Esperienza personalizzata</h2>
        <i class="fa-solid fa-quote-left"></i>
        <p class="fs-4">
          Crediamo che ogni cliente sia unico e meriti un'esperienza
          personalizzata. I nostri mixologist sono pronti ad ascoltare le
          vostre preferenze e consigliarvi i cocktail che meglio si adattano
          ai vostri gusti e alle vostre occasioni speciali.
        </p>
        <i class="fa-solid fa-quote-right"></i>
      </div>
    </div>
    <div class="py-5 d-flex gap-5 justify-content-center">
      <img
        style="
          width: 500px;
          box-shadow: rgba(151, 65, 252, 0.2) -30px -15px 160px 60px;
          border-radius: 30px;
        "
        src="../../public/drink-experience.jpg"
        alt=""
      />
      <img
        style="
          width: 500px;
          box-shadow: rgba(151, 65, 252, 0.2) -30px -15px 160px 60px;
          border-radius: 30px;
        "
        src="../../public/drink-experience-2.jpg"
        alt=""
      />
    </div>

    <div class="py-3 my-3 assapora">
      <div class="py-3">
        <div class="container text-center">
          <h2>Assaporate il piacere</h2>
          <i class="fa-solid fa-quote-left"></i>
          <p class="fs-4">
            Unitevi a noi in questo viaggio attraverso i sapori e le creazioni
            uniche. Sia che stiate cercando un'esperienza rilassante con gli
            amici, un modo per festeggiare un'occasione speciale o semplicemente
            vogliate scoprire nuovi gusti, il nostro sito di cocktail è il luogo
            perfetto per soddisfare tutti i vostri desideri.
          </p>
          <i class="fa-solid fa-quote-right"></i>
        </div>
      </div>
    </div>

    <div class="container py-3 my-1">
      <div class="text-center">
        <i class="fa-solid fa-quote-left"></i>
        <h3 style="font-style: italic">
          Gustate ogni goccia e lasciatevi conquistare dall'arte dei cocktail.
          Benvenuti nel nostro mondo, dove la mixology diventa un'esperienza di
          piacere senza fine...
        </h3>
        <h2 style="color: rgba(151, 65, 252); font-style: italic">Salute!</h2>
        <i class="fa-solid fa-quote-right"></i>
      </div>
    </div>
    
    <div class="py-5 d-flex justify-content-center">
      <button>
      <router-link class="text-decoration-none" :to="{ name: 'drinks' }"
        >I nostri cocktails</router-link
      >
    </button>
    </div>
    
  </div>
</template>

<style lang="scss" scoped>
$mainColor: #55328b;
.about {
  margin-top: 5rem;
  background-color: black;
  color: white;
}

.philosophy {
  height: 250px;
  height: 250px;
  border-radius: 20px;
  padding: 5px;
  box-shadow: rgba(151, 65, 252, 0.2) 0 15px 30px -5px;
  background-image: linear-gradient(144deg, #af40ff, #5b42f3 50%, #00ddeb);
}

.philosophy__content {
  background: rgb(5, 6, 45);
  border-radius: 17px;
  width: 100%;
  height: 100%;
}

.assapora {
  height: 600px;
  background-image: url(../../public/drink-assapora.jpg);
  background-position-y: -300px;
  border-top: 5px solid rgba(151, 65, 252, 0.2);
  border-bottom: 5px solid rgba(151, 65, 252, 0.2);
  background-repeat: no-repeat;
}

h2 {
  font-style: italic;
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
