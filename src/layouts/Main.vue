<template>
  <div class="container">
    <!-- <ul>
      <li>
        <v-link href="/">Home</v-link>
        <v-link href="/about">About</v-link>
        <v-link href="/red">Red</v-link>
        <v-link href="/yellow">Yellow</v-link>
        <v-link href="/green">Green</v-link>
      </li>
    </ul> -->

    <div class="traffic-light">
      <div class="red" :class="isRed"></div>
      <div class="yellow" :class="isYellow"></div>
      <div class="green" :class="isGreen"></div>
    </div>
  </div>
</template>

<script>
import VLink from '../components/VLink.vue';

export default {
  components: {
    VLink,
  },
  computed: {
    isRed() {
      return {
        active: this.$root.currentRoute === '/red',
      };
    },
    isYellow() {
      return {
        active: this.$root.currentRoute === '/yellow',
      };
    },
    isGreen() {
      return {
        active: this.$root.currentRoute === '/green',
      };
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 15px 30px;
}

.traffic-light {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.traffic-light div {
  height: 100px;
  width: 100px;
}

.red {
  background-color: red;
}

.yellow {
  background-color: yellow;
}

.green {
  background-color: green;
}

.red,
.yellow,
.green {
  opacity: 0.2;
}

.active {
  opacity: 1;
}
</style>
