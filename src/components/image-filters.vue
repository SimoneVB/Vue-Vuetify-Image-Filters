
<template>
  <v-container
    style="width:1210px;"
  >
    <v-row
      class="text-center"
    >
      <v-col cols="12">
        <v-img
          :src="image_url"
          class="my-3"
          contain
          height="600"
          :style="`filter: ${filter}`"
        />
      </v-col>

      <v-col cols="12">
        Choose an effect
        <v-btn-toggle
          v-model="effect"
          divided
          class="ml-2"
        >
          <v-btn
            v-for="(effect, index) in effects"
            :key="index"
          >{{ effect.name }}</v-btn>
        </v-btn-toggle>
      </v-col>

      <v-col cols="12">
        <!-- % slider -->
        <v-slider
          v-if="currentEffect.uom === '%'"
          v-model="percentage"
          :min="0"
          :max="200"
          :step="5"
          thumb-label="always"
          show-ticks="always"
          tick-size="5"
        >
          <template v-slot:thumb-label="{ modelValue }">
            {{ modelValue }}%
          </template>
        </v-slider>

        <!-- degrees slider -->
        <v-slider
          v-if="currentEffect.uom === 'deg'"
          v-model="degrees"
          :min="0"
          :max="360"
          :step="10"
          thumb-label="always"
          show-ticks="always"
          tick-size="10"
        >
          <template v-slot:thumb-label="{ modelValue }">
            {{ modelValue }}°
          </template>
        </v-slider>

        <!-- pixels slider -->
        <v-slider
          v-if="currentEffect.uom === 'px'"
          v-model="pixels"
          :min="0"
          :max="10"
          :step="1"
          thumb-label="always"
          show-ticks="always"
          tick-size="1"
        >
          <template v-slot:thumb-label="{ modelValue }">
            {{ modelValue }}px
          </template>
        </v-slider>
      </v-col>

    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'image-filters',

  data() {
    return {
      image_url: 'https://laopinion.com/wp-content/uploads/sites/3/2022/09/shutterstock_1696821382.jpg?quality=80&strip=all&w=1200',
      effect: 0,      // current effect
      effects: [      // supported effects
        {
          name: 'none',
        },
        {
          name: 'brightness',
          uom: '%'
        },
        {
          name: 'contrast',
          uom: '%'
        },
        {
          name: 'invert',
          uom: '%'
        },
        {
          name: 'opacity',
          uom: '%'
        },
        {
          name: 'saturate',
          uom: '%'
        },
        {
          name: 'hue-rotate',
          uom: 'deg'
        },
        {
          name: 'sepia',
          uom: '%'
        },
        {
          name: 'grayscale',
          uom: '%'
        },
        {
          name: 'blur',
          uom: 'px'
        },
        {
          name: 'drop-shadow',
          uom: 'px'
        },
      ],
      percentage: 100,
      degrees: 90,
      pixels: 0,
    }
  },

  computed: {
    currentEffect() {
      // returns the currently selected effect
      return this.effects[this.effect]
    },
    filter() {
      if (this.effect === 0) return 'none'

      let value = 0
      switch (this.currentEffect.uom) {
        case '%':
          value = this.percentage
          break
        case 'i': value = this.integer
          break
        case 'deg': value = this.degrees
          break
        case 'px': value = this.pixels
          break
      }
      if (this.currentEffect.name === 'drop-shadow') {
        return `${this.currentEffect.name}(${value}px ${value}px ${value}px gray)`
      } else {
        return `${this.currentEffect.name}(${value}${this.currentEffect.uom !== 'i' ? this.currentEffect.uom : ''})`
      }
    }
  }
}
</script>
