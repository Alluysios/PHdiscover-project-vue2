<template>
  <div class="home">
    <div class="destination">
      <h1>Discover Philippines</h1>
      <DestinationList v-bind:trails="trails" v-on:latlng="viewMapMarker" />
    </div>
    <div class="map">
      <Map v-bind:trails="trails" v-on:newTrail="newTrail" v-bind:markerPosition="this.markerPosition" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Map from '@/components/Map.vue';
import DestinationList from '@/components/DestinationList.vue';
export default {
  name: 'Home',
  data() {
    return {
      markerPosition: null,
      show: false,
      trails: [
        {
          id: 1321321,
          name: 'Busay',
          island: 'Cebu',
          type: 'Restaurant',
          popular: 'Very Popular',
          latlng: [10.362178, 123.881712]
        },
        {
          id: 125132,
          name: 'Naga Baywalk',
          island: 'Cebu',
          type: 'Walk, Jogging',
          popular: 'Extremely Popular',
          latlng: [10.208657, 123.760679]
        },
        {
          id: 54221,
          name: 'SM Seaside City',
          island: 'Cebu',
          type: 'Mall',
          popular: 'Extremely Popular',
          latlng: [10.281803, 123.879710]
        }
      ]
    }
  },
  components: {
    Map,
    DestinationList
  },
  methods: {
    viewMapMarker(latlng) {
      this.markerPosition = latlng;
    },
    newTrail(trail) {
      this.trails = [...this.trails, trail]
    }
  }
}
</script>

<style scoped>
  .home {
    display: flex;
    height: 100vh;
    overflow: hidden;
  }
  .destination {
    flex: 1 0 30%;
    background: rgb(255, 255, 255);
  }
  .map {
    flex: 1 0 70%;
  }
  h1 {
    margin-top: 1rem;
    margin-left: .5rem;
  }
</style>
