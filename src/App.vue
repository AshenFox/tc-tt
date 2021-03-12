<template>
  <home v-if="currentRoute === '/'" />
  <about v-else-if="currentRoute === '/about'" />
  <not-found v-else />
</template>

<script>
import NotFound from './pages/NotFound';
import About from './pages/About';
import Home from './pages/Home';

const delays = {
  '/red': 10000,
  '/yellow': 1500,
  '/green': 15000,
};

/* let timer = false;
 */
export default {
  name: 'App',
  components: {
    Home: Home,
    About: About,
    NotFound: NotFound,
  },

  data() {
    return {
      currentRoute: window.location.pathname,
      prevRoute: false,
      timer: false,
    };
  },

  created() {
    window.addEventListener('popstate', (e) => {
      this.prevRoute = this.currentRoute;
      this.currentRoute = window.location.pathname;
    });

    this.switchRoute();
  },

  updated() {
    /* console.log(this.prevRoute, this.currentRoute); */
    /* this.switchRoute(); */
  },

  methods: {
    switchRoute() {
      clearTimeout(this.timer);

      this.timer = setTimeout(() => {
        const nextRoute = this.next();

        this.prevRoute = this.currentRoute;
        this.currentRoute = nextRoute;
        window.history.pushState(null, this.currentRoute, this.currentRoute);

        /* console.log('switchRoute', this.currentRoute, this.prevRoute); */
      }, delays[this.currentRoute]);
    },

    next() {
      const { currentRoute, prevRoute } = this;

      /* console.log('==========');

      console.log(currentRoute, prevRoute); */

      let result;

      if (currentRoute === '/red' || currentRoute === '/green') result = '/yellow';
      if (currentRoute === '/yellow') {
        if (prevRoute === '/red') {
          result = '/green';
        } else;
        if (prevRoute === '/green') {
          result = '/red';
        } else if (!prevRoute) {
          return '/green';
        }
      }

      /* console.log(result);

      console.log('=========='); */

      return result;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  background-color: #555;
}
</style>
