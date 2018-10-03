<template>
  <div class="wrapper">
    <GlobalEvents 
      @keyup.left="goPrev()" 
      @keyup.right="goNext()"/>
    <div 
      :class="[prevTransition ? 'prev-transition' : '', nextTransition ? 'next-transition' : '']"
      class="grid" 
    >
      <nav>
        <img 
          src="images/logo.png" 
          alt="">
        <ul class="menu">
          <li class="phone">
            <a 
              href="tel:+4915776189789"
            ><i class="fa fa-phone" /> +49 (0) 1577 61 89 789</a>
          </li>
          <li class="mail">
            <a 
              href="mailto:info@jetzt-punkt-design.de"
            ><i class="fa fa-envelope" /> info@jetzt-punkt-design.de</a>
          </li>
        </ul>
      </nav>
      <main>
        <div class="logo">JETZT.Design</div>
        <div class="headline">
          <h1>Joscha Ziegeler</h1>
          <h2>Frontend-Entwickler</h2>
        </div>
      </main>
      <div class="projects">
        <div class="project p1">
          <h3>{{ projects[actualProject].title }} 
            <a 
              :href="projects[actualProject].url" 
              title=""
              target="_blank">
              <i class="fa fa-external-link-alt fa-xs" />
            </a>
          </h3>
          <div class="container">
            <img 
              :src="projects[actualProject].image"
              class="real-image"
              alt="">
            <img 
              :src="projects[prevProject].image"
              class="prev-image"
              alt="">
            <img 
              :src="projects[actualProject].image"
              class="act-image"
              alt="">
            <img
              :src="projects[nextProject].image"
              class="next-image"
              alt="">
            <div 
              class="description" 
              v-html="projects[actualProject].description"/>
          </div>
        </div>
        <div class="project p2">
          <h3>{{ projects[nextProject].title }}</h3>
          <div class="container">
            <img 
              :src="projects[nextProject].image"
              class="real-image"
              alt="">
            <img 
              :src="projects[actualProject].image"
              class="prev-image"
              alt="">
            <img 
              :src="projects[nextProject].image"
              class="act-image"
              alt="">
            <img
              :src="projects[nextNextProject].image"
              class="next-image"
              alt="">
          </div>
        </div>
      </div>
      <div class="project-nav">
        <a 
          class="prev"
          @click="goPrev()"
        >
          <i class="fas fa-chevron-left fa-2x" />
        </a>
        <a 
          class="next" 
          @click="goNext()"
        >
          <i class="fas fa-chevron-right fa-2x" />
        </a>
      </div>
      <div class="portrait">
        <img 
          src="~/assets/portrait.png"
          alt="">
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import GlobalEvents from 'vue-global-events'

export default {
  components: {
    Logo,
    GlobalEvents
  },
  data() {
    return {
      nextTransition: false,
      prevTransition: false,
      actualProject: 0,
      projects: [
        {
          title: 'Grillexperten',
          image: 'images/grillexperten.jpg',
          url: 'https://www.grillexperten.de',
          description: '<strong>Konzeption, Design & Umsetzung</strong>'
        },
        {
          title: 'Kloster Maihingen',
          image: 'images/kloster-maihingen.jpg',
          url: 'https://www.kloster-maihingen.de',
          description: '<strong>Umsetzung</strong>'
        },
        {
          title: "Beit Al Liqa'",
          image: 'images/beit-al-liqa.jpg',
          url: 'https:/beit-al-liqa.de',
          description: '<strong>Konzeption, Design & Umsetzung</strong>'
        },
        {
          title: 'Gartenmöbel Experten',
          image: 'images/gartenmoebel-experten.jpg',
          url: 'https://www.gartenmoebel-experten.de',
          description: '<strong>Konzeption, Design & Umsetzung</strong>'
        },
        {
          title: 'Gärtner Coaching',
          image: 'images/gaertnercoaching.jpg',
          url: 'http://www.gaertnercoaching.de',
          description: '<strong>Umsetzung</strong>'
        },
        {
          title: 'Sola Hannover',
          image: 'images/sola-hannover.jpg',
          url: 'https://www.sola-hannover.de',
          description: '<strong>Konzeption, Design & Umsetzung</strong>'
        },
        {
          title: 'IdiSB e.V.',
          image: 'images/idisb.jpg',
          url: 'https://www.idisb.de',
          description: '<strong>Konzeption, Design & Umsetzung</strong>'
        }
      ]
    }
  },
  computed: {
    nextProject() {
      // prettier-ignore
      return this.actualProject === (this.projects.length - 1) ? 0 : this.actualProject + 1;
    },
    nextNextProject() {
      // prettier-ignore
      if(this.actualProject === (this.projects.length - 2)){
        return 0;
      } else if (this.actualProject === (this.projects.length - 1)){
        return 1
      } else {
        return this.actualProject + 2;
      }
    },
    prevProject() {
      // prettier-ignore
      return this.actualProject === 0 ? this.projects.length - 1 : this.actualProject - 1;
    }
  },
  methods: {
    goPrev() {
      console.log('prev')
      if (!this.nextTransition && !this.prevTransition) {
        this.prevTransition = true
        setTimeout(() => {
          // prettier-ignore
          this.actualProject = this.actualProject === 0 ? this.projects.length - 1 : this.actualProject - 1;
          this.prevTransition = false
        }, 1200)
      }
    },
    goNext() {
      if (!this.nextTransition && !this.prevTransition) {
        this.nextTransition = true
        setTimeout(() => {
          // prettier-ignore
          this.actualProject = this.actualProject === (this.projects.length - 1) ? 0 : this.actualProject + 1;
          this.nextTransition = false
        }, 1200)
      }
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Heebo:100,300,400,500,700,800,900');
.wrapper {
  max-width: 100%;
  overflow: hidden;
  font-family: 'Heebo';
}
.grid {
  display: grid;
  grid-template-columns: 80px 5fr 160px 2fr;
  grid-template-rows: 1fr 1fr;
  height: 100vh;
}
.portrait {
  grid-row: 2 / 4;
  grid-column: 4 / 5;
  position: relative;
  z-index: 10;
  img {
    max-height: 70vh;
    position: absolute;
    bottom: 0;
    right: 0;
  }
}
nav {
  background: #fff;
  grid-row: 1 / 4;
  display: flex;
  flex-direction: column;
  align-items: center;
  img {
    max-width: 80%;
    padding-top: 5px;
  }
  .menu {
    list-style-type: none;
    margin: 0;
    padding: 0;
    position: absolute;
    top: 150px;
    transform: rotate(-90deg);
    li {
      padding-bottom: 4px;
    }
    a {
      font-weight: 900;
      text-decoration: none;
      color: #870a4f;
    }
    i {
      transform: rotate(90deg);
    }
    .mail {
      min-width: 240px;
    }
    .phone {
      min-width: 210px;
    }
  }
}
main {
  background: linear-gradient(to right, #e41a62, #8b4590);
  grid-row: 1 / 4;
  grid-column: 2 / 5;
  color: #fff;
  padding-right: 80px;
  padding-top: 40px;
}
.logo {
  position: absolute;
  top: 17px;
  left: 93px;
  font-size: 31px;
  font-weight: 700;
  opacity: 0.5;
}
.headline {
  text-align: right;
}
h1 {
  font-family: 'Heebo';
  // font-family: 'Audiowide';
  // font-family: 'Expletus Sans';
  // font-family: 'Press Start 2P';
  font-size: 10vh;
  font-weight: 900;
}
h2 {
  // font-family: 'Audiowide';
  font-family: 'Heebo';
  font-size: 6vh;
  font-weight: 300;
  text-align: right;
}

.projects {
  grid-row: 2 / 3;
  grid-column: 2 / 3;
  display: flex;
  width: calc(200% + 160px);
}
.project {
  flex-basis: 90vh;
  position: relative;
  flex-basis: 100%;
  h3 {
    color: #fff;
    padding-left: 20px;
    padding-bottom: 10px;
    position: absolute;
    top: -45px;
    font-size: 30px;
    font-weight: 500;
    transition: all 0.3s;
    a {
      color: #870a4f;
    }
  }
  .container {
    height: 100%;
    max-height: 100%;
    width: 100%;
    position: relative;
    overflow: hidden;
  }
  img {
    object-fit: cover;
    object-position: top left;
    width: 100%;
    height: 100%;
    display: block;
    position: absolute;
    transition: left 1.2s, right 1.2s;
  }
  .real-image {
    z-index: 8;
  }
  .act-image {
    top: 0;
    left: 0;
    right: 0;
    z-index: 2;
  }
  .prev-image {
    top: 0;
    left: calc(-100% - 160px);
    z-index: 2;
  }

  .next-image {
    top: 0;
    right: calc(-100% - 160px);
    z-index: 2;
  }
}
.prev-transition {
  .real-image {
    opacity: 0;
  }
  h3 {
    opacity: 0;
    top: 0;
  }

  .act-image {
    right: calc(-100% - 160px);
    left: auto;
  }

  .prev-image {
    left: 0;
  }
}

.next-transition {
  .real-image {
    opacity: 0;
  }
  h3 {
    opacity: 0;
    top: 0;
  }

  .act-image {
    left: calc(-100% - 160px);
    right: auto;
  }

  .next-image {
    right: 0;
  }
}

.p1 {
  margin-right: 160px;
}
.p2 {
  opacity: 0.3;
}
.project-nav {
  grid-column: 3 / 4;
  grid-row: 2 / 3;
  align-self: end;
  display: flex;
  margin-left: -80px;
  z-index: 15;
  a {
    width: 80px;
    height: 80px;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: bold;
    &:hover {
      cursor: pointer;
    }
  }
  .prev {
    background: #c10859;
  }
  .next {
    background: #870a4f;
  }
}
.description {
  color: #fff;
  height: 0%;
  width: 40%;
  top: 50%;
  left: 30%;
  background: rgba(135, 10, 79, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  z-index: 10;
  opacity: 0;
  transition: all 0.3s;
}
.container:hover .description {
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  opacity: 1;
}
</style>
