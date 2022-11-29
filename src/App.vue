<template>
  <div id="app">
    <div class="nav">
      <div class="nav__title">midbra.in</div>
      <div class="nav__menu">
<!--        <div class="nav__menu__item">sections</div>-->
        <div class="nav__menu__item">how to</div>
        <div class="nav__menu__item">namings</div>
      </div>
    </div>
    <div class="how-to" v-if="howTo">
      <div class="how-to__text">
        Hi!
        welcome to <span>midbra.in</span>!
        to learn about the brain just scroll the page and search click on the brain parts you know.
        at the end you will be able to see what you guessed wrong or didn't guess at all.
        <span>if you guessed something wrong and then corrected it - it will appear as wrong</span>
      </div>
    </div>
    <div @click="notDone" v-if="isDone" class="results__close">
      close
    </div>
    <div class="results" v-if="isDone">
      <div class="results__headers">
        <div @click="openTab('coronal')" class="results__headers__header__coronal">{{ coronalDone.who }}</div>
        <div class="results__spec" v-if="currOpen === 'coronal'">
          <div class="results__spec__rights">
            <div class="results__spec__rights__title">RIGHTS</div>
            <div class="results__spec__rights__items">
              <div class="results__spec__rights__items__item" v-for="item in coronalDone.rights" :key="item">
                {{ item }}
              </div>
            </div>
          </div>
          <div class="results__spec__wrongs">
            <div class="results__spec__wrongs__title">WRONGS</div>
            <div class="results__spec__wrongs__items">
              <div class="results__spec__wrongs__items__item" v-for="item in coronalDone.wrongs" :key="item">
                {{ item }}
              </div>
            </div>
          </div>
        </div>
        <div @click="openTab('lateral')" class="results__headers__header__lateral">{{ lateralDone.who }}</div>
        <div class="results__spec" v-if="currOpen === 'lateral'">
          <div class="results__spec__rights">
            <div class="results__spec__rights__title">RIGHTS</div>
            <div class="results__spec__rights__items">
              <div class="results__spec__rights__items__item" v-for="item in lateralDone.rights" :key="item">
                {{ item }}
              </div>
            </div>
          </div>
          <div class="results__spec__wrongs">
            <div class="results__spec__wrongs__title">WRONGS</div>
            <div class="results__spec__wrongs__items">
              <div class="results__spec__wrongs__items__item" v-for="item in lateralDone.wrongs" :key="item">
                {{ item }}
              </div>
            </div>
          </div>
        </div>
        <div @click="openTab('sagittal')" class="results__headers__header__sagittal">{{ sagittalDone.who }}</div>
        <div class="results__spec" v-if="currOpen === 'sagittal'">
          <div class="results__spec__rights">
            <div class="results__spec__rights__title">RIGHTS</div>
            <div class="results__spec__rights__items">
              <div class="results__spec__rights__items__item" v-for="item in sagittalDone.rights" :key="item">
                {{ item }}
              </div>
            </div>
          </div>
          <div class="results__spec__wrongs">
            <div class="results__spec__wrongs__title">WRONGS</div>
            <div class="results__spec__wrongs__items">
              <div class="results__spec__wrongs__items__item" v-for="item in sagittalDone.wrongs" :key="item">
                {{ item }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <coronalSection @done="setDone" ref="coronal" class="coronalSection"></coronalSection>
    <sagittalSection @done="setDone" ref="sagittal" class="sagittalSection"></sagittalSection>
    <lateralSection @done="setDone" ref="lateral" class="lateralSection"></lateralSection>
    <div class="done-button" @click="getDoneStatus">DONE</div>
    <div @click="goToURL" class="spotify-playlist">
      <svg xmlns="http://www.w3.org/2000/svg" height="50px" width="50px" viewBox="0 0 168 168">
        <path
            d="m83.996 0.277c-46.249 0-83.743 37.493-83.743 83.742 0 46.251 37.494 83.741 83.743 83.741 46.254 0 83.744-37.49 83.744-83.741 0-46.246-37.49-83.738-83.745-83.738l0.001-0.004zm38.404 120.78c-1.5 2.46-4.72 3.24-7.18 1.73-19.662-12.01-44.414-14.73-73.564-8.07-2.809 0.64-5.609-1.12-6.249-3.93-0.643-2.81 1.11-5.61 3.926-6.25 31.9-7.291 59.263-4.15 81.337 9.34 2.46 1.51 3.24 4.72 1.73 7.18zm10.25-22.805c-1.89 3.075-5.91 4.045-8.98 2.155-22.51-13.839-56.823-17.846-83.448-9.764-3.453 1.043-7.1-0.903-8.148-4.35-1.04-3.453 0.907-7.093 4.354-8.143 30.413-9.228 68.222-4.758 94.072 11.127 3.07 1.89 4.04 5.91 2.15 8.976v-0.001zm0.88-23.744c-26.99-16.031-71.52-17.505-97.289-9.684-4.138 1.255-8.514-1.081-9.768-5.219-1.254-4.14 1.08-8.513 5.221-9.771 29.581-8.98 78.756-7.245 109.83 11.202 3.73 2.209 4.95 7.016 2.74 10.733-2.2 3.722-7.02 4.949-10.73 2.739z"/>
      </svg>

    </div>
  </div>
</template>

<script>
import coronalSection from '@/components/coronalSection'
import sagittalSection from '@/components/sagittalView'
import lateralSection from '@/components/lateralSection'

export default {
  name: 'App',
  components: {
    coronalSection,
    sagittalSection,
    lateralSection
  },
  data() {
    return {
      isDone: false,
      coronalDone: null,
      lateralDone: null,
      sagittalDone: null,
      currOpen: null,
    }
  },
  methods: {
    goToURL() {
      window.open("https://open.spotify.com/playlist/6nhkfZ1IsWrWUjB2tfat5S?si=beb9c10d2e12401b&pt=8f111dfc522e7f15fde83e2d9ffdea3c", "_blank")
    },
    setDone(payload) {
      if (payload.who === "coronal") {
        this.coronalDone = payload;
      }
      if (payload.who === "lateral") {
        this.lateralDone = payload;
      }
      if (payload.who === "sagittal") {
        this.sagittalDone = payload;
      }
      this.isDone = true;
    },
    getDoneStatus() {
      this.$refs.lateral.getDone()
      this.$refs.sagittal.getDone()
      this.$refs.coronal.getDone()
    },
    openTab(payload) {
      if (payload === "coronal") {
        this.currOpen = this.currOpen === "coronal" ? null : "coronal"
      }
      if (payload === "sagittal") {
        this.currOpen = this.currOpen === "sagittal" ? null : "sagittal"
      }
      if (payload === "lateral") {
        this.currOpen = this.currOpen === "lateral" ? null : "lateral"
      }
    },
    notDone() {
      this.isDone = false;
      this.$refs.lateral.reset()
      this.$refs.sagittal.reset()
      this.$refs.coronal.reset()
      window.scrollTo(0, 0);

    }
  },
  watch: {
    isDone: {
      handler() {
        if (this.isDone) {
          document.body.style.overflow = "hidden";
          // document.querySelector(".coronalSection").classList.add("modalOpen")
          // document.querySelector(".lateralSection").classList.add("modalOpen")
          // document.querySelector(".sagittalSection").classList.add("modalOpen")
          // document.querySelector(".spotify-playlist").classList.add("modalOpen")
          document.querySelector(".done-button").classList.add("hidden")
        } else {
          document.body.style.overflow = "auto";
          document.querySelector(".coronalSection").classList.remove("modalOpen")
          document.querySelector(".lateralSection").classList.remove("modalOpen")
          document.querySelector(".sagittalSection").classList.remove("modalOpen")
          document.querySelector(".spotify-playlist").classList.remove("modalOpen")
          document.querySelector(".done-button").classList.remove("hidden")
        }
      }
    }
  },
  mounted() {
    window.addEventListener("scroll", function() {
      if (document.documentElement.scrollTop > 80) {
        document.querySelector(".nav").style.height = "40px";
      } else {
        document.querySelector(".nav").style.height = "80px";

      }
      })
  }
}
</script>

<style lang="scss">
@import "styles/_variables";
@import url("https://use.typekit.net/wmf5gqb.css");

html {
  scroll-behavior: smooth;
}

* {
  box-sizing: border-box;
  margin: 0;
}

#app {
  //background-image: linear-gradient(120deg, #fdfbfb 0%, #ebedee 100%);
}

.nav {
  height: 80px;
  background-color: white;
  box-shadow: 0 2px 0 0 $color-outline;
  top: 0;
  width: 100%;
  position: sticky;
  display: flex;
  padding: 0 80px;
  justify-content: space-between;
  place-items: center;
  transition: height 0.2s ease;

  &__title{
    font-family: Cy, sans-serif;
    font-weight: 400;
    font-size: 22px;
    transition: font-weight 0.2s ease;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    &:hover {
      font-weight: 900;
    }
  }

  &__menu {
    width: 200px;
    font-family: Cy, sans-serif;
    font-weight: 400;
    font-size: 22px;
    transition: font-weight 0.2s ease;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    cursor: pointer;

    &__item {
      &:hover {
        font-weight: 900;
      }
    }
  }
}

#app {
  display: flex;
  flex-direction: column;
  align-content: center;
  align-items: center;
}

.coronalSection {
  width: 100vw;
  height: 100vh;
}

.sagittalSection {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.lateralSection {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.spotify-playlist {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 50px;
  height: 50px;
  /*background: black;*/
  cursor: pointer;
  fill: #1ED760;

  &:hover {
    fill: #ff757e;
  }
}

.done-button {
  width: 400px;
  height: 100px;
  cursor: pointer;
  font-family: Cy, sans-serif;
  font-weight: 700;
  font-size: 32px;
  border-radius: 20px;
  border: 2px solid black;
  padding: 20px;
  background-color: #3A2D32;
  color: #fff;
  display: flex;
  place-items: center;
  place-content: center;
  transition: all 0.2s ease;
  margin-top: 40px;
  margin-bottom: 20px;



  &:hover {
    background-color: #3A2C35;
    font-weight: 900;
    transition: all 0.2s ease;
  }
}

.results__close {
  font-family: Cy, sans-serif;
  position: fixed;
  color: #aaa;
  font-weight:400;
  top: 60px;
  right: 80px;

  &:hover, :focus {
    color: black;
    font-weight:800;
  }
}

.results {
  position: fixed;
  display: flex;
  place-items: center;
  z-index: 2;
  width: 80vw;
  height: 80vh;
  background-color: #b2fcbb;
  border: 4px solid $color-outline;
  border-radius: 20px;
  align-items: flex-start;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  overflow: auto;

  &__headers {
    display: flex;
    flex-direction: column;
    position: sticky;
    width: 100%;
    place-items: center;
    place-content: center;
    font-family: Cy, sans-serif;

    &__header {
      height: 200px;
      font-size: 60px;
      display: flex;
      position: sticky;
      place-items: center;
      place-content: center;
      box-shadow: 0 2px 0 0 black;
      width: 100%;

      &__coronal {
        height: 200px;
        font-size: 60px;
        display: flex;
        position: sticky;
        place-items: center;
        place-content: center;
        box-shadow: 0 2px 0 0 black;
        width: 100%;
        top: 0;
        background-color: #b2fcbb;
        z-index: 3;

        &:hover {
          font-weight: 900;
        }

      }

      &__lateral {
        height: 200px;
        font-size: 60px;
        display: flex;
        position: sticky;
        place-items: center;
        place-content: center;
        box-shadow: 0 2px 0 0 black;
        width: 100%;
        top: min(200px);
        background-color: #b2fcbb;
        z-index: 2;

        &:hover {
          font-weight: 900;
        }
      }

      &__sagittal {
        height: 200px;
        font-size: 60px;
        display: flex;
        position: sticky;
        place-items: center;
        place-content: center;
        box-shadow: 0 2px 0 0 black;
        width: 100%;
        top: min(400px);
        background-color: #b2fcbb;
        z-index: 1;

        &:hover {
          font-weight: 900;
        }
      }

    }
  }

  &__spec {
    display: flex;
    width: 80%;
    justify-content: space-between;
    padding-bottom: 20px;

    &__rights {
      &__title {
        font-size: 60px;
        font-weight: 900;
      }

      &__items {
        font-size: 24px;
        overflow: auto;
      }
    }

    &__wrongs {
      &__title {
        font-size: 60px;
        font-weight: 900;
      }

      &__items {
        font-size: 24px;
      }
    }
  }
}

.modalOpen {
  backdrop-filter: blur(2px);
}

.hidden {
  transition: all 0.2s ease;
  visibility: hidden;
}
</style>
