<template>
  <div >
    <h3>How much do you weigh?</h3>
    <div>
      <vue-slider 
        class="slider"
        ref="slider" 
        v-model="weight" 
        formatter="{value} kg" 
        :min="35"
        :max="120"
        :tooltip-style="{'background-color': '#2d616f', 'border-color': '#2d616f'}"
        :process-style="{'background-color': '#2d616f'}"
        @callback="compute()">
      </vue-slider>
    </div>
    <h3>What do you travel with?</h3>
    <p class="buttons">
      <a class="button" @click="vehicle={'type': 'pedestrian', 'weight': 0}; compute()">
        <span class="icon">
          <i class="fas fa-walking"></i>
        </span>
        <span>Nothing</span>
      </a>
      <a class="button is-primary" @click="vehicle={'type': 'semi-trailer', 'weight': 30000}; compute()">
        <span class="icon">
          <i class="fas fa-truck-moving"></i>
        </span>
        <span>Semi-trailer</span>
      </a>
      <a class="button is-success" @click="vehicle={'type': 'truck', 'weight': 5000}; compute()">
        <span class="icon">
          <i class="fas fa-truck"></i>
        </span>
        <span>Truck</span>
      </a>
      <a class="button is-info" @click="vehicle={'type': 'car', 'weight': 1200}; compute()">
        <span class="icon">
          <i class="fas fa-car-side"></i>
        </span>
        <span>Car</span>
      </a>
      <a class="button is-link" @click="vehicle={'type': 'bicycle', 'weight': 15}; compute()">
        <span class="icon">
          <i class="fas fa-bicycle"></i>
        </span>
        <span>Bicycle</span>
      </a>
    </p>
    <h3>Your lethal speed in km/h&nbsp;<span class="is-size-6">Mind the logarithmic scale!</span></h3>
    <div class="speed-bar">
      <div class="columns is-mobile legend-scale is-size-7">
        <div class="column has-text-left">1 km/h</div>
        <div class="column has-text-left">2 km/h</div>
        <div class="column has-text-left">10 km/h</div>
        <div class="column has-text-right">100 km/h</div>
      </div>
      <div class="columns is-mobile speed-scale">
        <div class="column has-text-left is-narrow is-accident" :style="styleSpeed"></div>
        <div class="column is-one-fifth speed-sign">
          <div class="speed-sign-text">
            {{ Math.round(speed) }}
          </div>
        </div>
        <div class="column has-text-left is-not-accident is-hidden-mobile">
          <div class="is-not-accident-text is-size-7">
            An impact between a pedestrian and a {{ vehicle.type }} over {{ Math.round(speed) }}km/h will cause severe injury.
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import vueSlider from 'vue-slider-component'
  export default {
    name: 'Calculator',
    components: {
      vueSlider
    },
    data () {
      return {
        weight: 65,
        speed: 12,
        vehicle: {'type': 'car', 'weight': 1200}
      }
    },
    computed: {
      styleSpeed() {
        return {
            'width': Math.log10(this.speed) * 50 + '%'
          }
      }
    },
    methods: {
      compute() {
        // Applies E = 1/2 * m * v² and converts m/s to km/h
        this.speed = Math.sqrt(( 2 * 6800)/(this.weight + this.vehicle.weight)) * 3.6
        this.$emit('callback', {weight: this.weight, vehicle: this.vehicle, speed: this.speed})
      }
    }
  }
</script>

<style lang="sass" scoped>
@import "colors.sass"

.speed-bar
  margin-bottom: 2rem

.speed-scale
  width: 80%

.legend-scale
  width: 85%
  font-family: Arial, sans-serif

.speed-sign
  border-radius: 150px
  width: 60px !important
  height: 60px !important
  border: 8px solid $nkb-red
  text-align: center
  background-color: white

.speed-sign-text
  font-family: Arial, sans-serif
  font-weight: bold
  margin-top: -20%
  width: 140%
  margin-left: -20%
  font-size: 1.4em

.slider
  margin-top: 4rem

.is-accident
  transition: all 0.5s ease-out;

.is-not-accident
  min-width: 30%
  position: relative
  background-color: $nkb-red
  background-image: linear-gradient(to right, $nkb-red, black);
  height: 5rem
  margin-top: -.7rem
  z-index: -1
  margin-left: -2rem
  transform: skewX(-10deg)

.is-not-accident-text
  font-family: Arial, sans-serif
  transform: skewX(10deg)
  padding-left: 20%
  color: white
  line-height: 1rem
</style>
