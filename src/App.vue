<template>
    <ion-router-outlet :key="$route.fullPath" style="overflow-y: scroll" />
</template>

<script>
import {
  IonRouterOutlet } from '@ionic/vue';
import { defineComponent } from 'vue';
const P5 = require('p5')

export default defineComponent({
  name: 'App',
  components: {
    IonRouterOutlet,
  },
  data(){
    return {
      grid:[],
      color_stard_for :{},
      resolution:0,
      square_length:window.screen.width<540?window.screen.width:540,
      P5_obj : {},
    }
  },
  methods:{
    sketch(p){
      const _this = this
      const grid = _this.grid
      const square_length = this.square_length

      p.setup = () => {
        let canvas = p.createCanvas(
            square_length,square_length
        );
        canvas.position((window.screen.width -square_length)/2, 0)
        window.document.getElementsByTagName('canvas')[0].style.zIndex=-3
      }

      p.draw = () => {
        p.background(0);
        if (_this.$route.path!=='/mint'){
          p.noStroke();
        }
        let resolution = _this.resolution
        for (let i = 0; i < grid.length; i++) {
          for (let j = 0; j < grid[0].length; j++) {
            let x = j * resolution
            let y = i * resolution

            p.fill(_this.color_stard_for[grid[i][j]])
            p.rect(x, y, resolution, resolution,resolution/16)
          }
        }
      }
    },
  },
  mounted(){
    if(this.$route.path==='/mint'){
      const [pi, c, s, l, t] = ['pillar', 'cloud', 'sun', 'leaf', 'tree']
      this.resolution = this.square_length/18
      this.grid = [
        [pi, 1, 1, 1, 1,   1, 1, 1, 1, 1,  1, 1, 1, 1, 1,  1, 1, pi],
        [1, 0, 0, s, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, c, c, s, s,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, c, c, c, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  c, c, 1],
        [1, c, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, c,  c, c, 1],

        [1, 0, 0, 0, 0,   0, 0, 0, 0,0,    0, 0, 0, 0, 0,  0, c, 1],
        [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],

        [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, 0, 0, l, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, 0, l, l, l,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, l, l, l, l,   l, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],

        [1, 0, 0, t, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [1, 0, 0, t, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
        [pi, 1, 1, 1, 1,   1, 1, 1, 1, 1,  1, 1, 1, 1, 1,  1, 1, pi],
      ]
      this.color_stard_for = {
        1: "#FFD2D2", 0: "#C8FBFE",
        pillar: "#FFA800", cloud: "#FFFFFF", sun: "#FDC840",
        leaf: "#90C86D", tree: "#9F6E52"
      }
    }
    else if (this.$route.path==='/land'){
      const [s1, s2, cl,
        g1, g2, g3,
        r1, r2, r3,
        e1, e2, e3,
      ] = ['sky_up', 'sky_down', 'cloud',
        'grass_some', 'grass_more', 'grass_a_lot',
        'rock_little', 'rock_greate', 'rock_huge',
        'earth_dry', 'earth_moist', 'earth_wet',
      ]
      this.resolution = this.square_length/36
      this.grid = [
        [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, cl, cl, cl, cl,   cl, cl, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
        [s1, s1, s1, s1, s1,   s1, s1, s1, cl, cl,   cl, cl, cl, cl, cl,   s1, s1, s1, s1, cl,   cl, cl, cl, cl, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
        [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, cl, cl,   cl, cl, cl, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
        [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, cl, cl, cl,   cl, cl, s1, s1, s1,   s1, s1, s1, s1, cl,   cl, cl, cl, cl, cl,   cl,],
        [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, cl, cl, cl,   cl, cl, cl, cl, cl,   cl,],

        [cl, cl, cl, cl, cl,   cl, cl, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, cl,   cl, cl, cl, cl, cl,   cl, cl, cl, cl, cl,   cl,],
        [cl, cl, cl, cl, cl,   cl, cl, cl, cl, cl,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, cl, cl,   cl, cl, cl, cl, cl,   cl,],
        [cl, cl, cl, cl, cl,   cl, cl, cl, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
        [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
        [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],

        [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
        [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
        [s2, s2, s2, s2, s2,   s2, s2, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s2, s2, s2, s2, s2,   s2,],
        [s2, s2, s2, s2, s2,   s2, s2, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s2, s2, s2, s2, s2,   s2,],
        [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],

        [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
        [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
        [g1, g1, g2, g1, g2,   g1, g1, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
        [r2, r3, r3, r2, r2,   r3, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
        [r3, r2, r2, r2, r3,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],

        [s2, s2, r3, r3, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, r1, r3, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
        [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, r2, r2, r2, r2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
        [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   r3, r2, r3, r3, r2,   r1, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
        [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, r1,   r2, r3, r2, r2, r3,   r2, r3, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
        [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, r3, r2,   r3, r2, r2, r3, r3,   r2, r2, r3, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],

        [g2, g1, g1, g2, g2,   g2, g2, g3, g2, g2,   g2, g1, g2, g2, g2,   g2, g2, g2, g2, g1,   g2, g3, g2, g2, g2,   g2, g2, g2, g1, g2,   g3, g2, g2, g3, g2,   g2,],
        [g2, g2, g2, g3, g2,   g1, g2, g1, g2, g3,   g2, g2, g3, g2, g3,   g2, g3, g2, g2, g2,   g2, g3, g2, g1, g2,   g2, g3, g3, g2, g1,   g2, g2, g2, g1, g2,   g3,],
        [g2, g3, g2, g2, g2,   g2, g3, g2, g2, g2,   g3, g2, g2, g1, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g3, g2,   g2, g2, g2, g2, g3,   g3, g2, g2, g2, g2,   g1,],
        [e1, e1, e3, e2, e1,   e2, e1, e1, e1, e1,   e1, e2, e1, e3, e1,   e1, e1, e1, e1, e1,   e1, e1, e3, e1, e1,   e1, e2, e1, e1, e3,   e1, e1, e1, e2, e1,   e1,],
        [e3, e1, e1, e1, e2,   e1, e1, e3, e1, e3,   e1, e3, e1, e1, e1,   e1, e1, e1, e1, e1,   e1, e1, e2, e1, e1,   e2, e1, e1, e1, e1,   e1, e2, e1, e3, e1,   e1,],

        [e1, e1, e1, e3, e1,   e1, e2, e1, e1, e1,   e1, e1, e1, e2, e1,   e1, e1, e1, e1, e1,   e1, e2, e1, e1, e3,   e1, e1, e3, e1, e1,   e2, e1, e1, e2, e1,   e2,],
        [e1, e1, e1, e1, e1,   e2, e1, e1, e1, e2,   e1, e1, e1, e3, e1,   e1, e1, e1, e1, e1,   e1, e1, e3, e1, e1,   e1, e2, e1, e1, e1,   e3, e1, e2, e1, e1,   e1,],
        [e3, e1, e2, e3, e1,   e3, e1, e1, e1, e1,   e1, e1, e1, e1, e1,   e2, e1, e1, e1, e1,   e2, e1, e2, e1, e2,   e1, e1, e1, e2, e1,   e1, e2, e1, e1, e3,   e1,],
        [e1, e1, e1, e1, e1,   e1, e1, e1, e1, e1,   e1, e3, e1, e1, e2,   e1, e1, e1, e1, e1,   e1, e1, e1, e1, e2,   e1, e1, e3, e1, e1,   e2, e1, e2, e1, e1,   e1,],
        [g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2,],

        [g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2,],

      ]
      this.color_stard_for = {
        sky_up: "#ABDBE8", sky_down: "#D2E6ED",
        cloud: "#FFFFFF",
        grass_some: "#91BA51", grass_more: "#83AB38", grass_a_lot: "#5A7C2F",
        rock_little: "#DED3D9", rock_greate: "#9E8E99", rock_huge: "#80747E",
        earth_dry: "#6D6452", earth_moist: "#635846", earth_wet: "#585149"
      }
    }
    else if (this.$route.path==='/roadmap'){
      const [e2,] = ['earth_moist',]
      this.resolution = this.square_length
      this.grid = [[e2,],]
      this.color_stard_for = {
        earth_moist: "#635846",
      }
    }
    else if (this.$route.path==='/whitepaper'){
      const [s1,] = ['sky_up',]
      this.resolution = this.square_length
      this.grid = [[s1,],]
      this.color_stard_for = {
        sky_up: "#ABDBE8",
      }
    }

    this.P5_obj = new P5(this.sketch,this.$route.path.substr(1))
  },
  watch: {
    '$route'(to) {
      if (to.path === '/mint') {
        const [pi, c, s, l, t] = ['pillar', 'cloud', 'sun', 'leaf', 'tree']
        this.resolution = this.square_length/18
        this.grid = [
          [pi, 1, 1, 1, 1,   1, 1, 1, 1, 1,  1, 1, 1, 1, 1,  1, 1, pi],
          [1, 0, 0, s, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, c, c, s, s,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, c, c, c, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  c, c, 1],
          [1, c, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, c,  c, c, 1],

          [1, 0, 0, 0, 0,   0, 0, 0, 0,0,    0, 0, 0, 0, 0,  0, c, 1],
          [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],

          [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, 0, 0, 0, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, 0, 0, l, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, 0, l, l, l,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, l, l, l, l,   l, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],

          [1, 0, 0, t, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [1, 0, 0, t, 0,   0, 0, 0, 0, 0,   0, 0, 0, 0, 0,  0, 0, 1],
          [pi, 1, 1, 1, 1,   1, 1, 1, 1, 1,  1, 1, 1, 1, 1,  1, 1, pi],
        ]
        this.color_stard_for = {
          1: "#FFD2D2", 0: "#C8FBFE",
          pillar: "#FFA800", cloud: "#FFFFFF", sun: "#FDC840",
          leaf: "#90C86D", tree: "#9F6E52"
        }
      }
      else if (to.path === '/land') {
        const [s1, s2, cl,
          g1, g2, g3,
          r1, r2, r3,
          e1, e2, e3,
        ] = ['sky_up', 'sky_down', 'cloud',
          'grass_some', 'grass_more', 'grass_a_lot',
          'rock_little', 'rock_greate', 'rock_huge',
          'earth_dry', 'earth_moist', 'earth_wet',
        ]
        this.resolution = this.square_length/36
        this.grid = [
          [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, cl, cl, cl, cl,   cl, cl, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
          [s1, s1, s1, s1, s1,   s1, s1, s1, cl, cl,   cl, cl, cl, cl, cl,   s1, s1, s1, s1, cl,   cl, cl, cl, cl, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
          [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, cl, cl,   cl, cl, cl, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
          [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, cl, cl, cl,   cl, cl, s1, s1, s1,   s1, s1, s1, s1, cl,   cl, cl, cl, cl, cl,   cl,],
          [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, cl, cl, cl,   cl, cl, cl, cl, cl,   cl,],

          [cl, cl, cl, cl, cl,   cl, cl, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, cl,   cl, cl, cl, cl, cl,   cl, cl, cl, cl, cl,   cl,],
          [cl, cl, cl, cl, cl,   cl, cl, cl, cl, cl,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, cl, cl,   cl, cl, cl, cl, cl,   cl,],
          [cl, cl, cl, cl, cl,   cl, cl, cl, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
          [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
          [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],

          [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
          [s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1,],
          [s2, s2, s2, s2, s2,   s2, s2, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s2, s2, s2, s2, s2,   s2,],
          [s2, s2, s2, s2, s2,   s2, s2, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s1, s1, s1, s1, s1,   s2, s2, s2, s2, s2,   s2,],
          [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],

          [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
          [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
          [g1, g1, g2, g1, g2,   g1, g1, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
          [r2, r3, r3, r2, r2,   r3, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
          [r3, r2, r2, r2, r3,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],

          [s2, s2, r3, r3, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, r1, r3, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
          [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, r2, r2, r2, r2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
          [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   r3, r2, r3, r3, r2,   r1, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
          [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, r1,   r2, r3, r2, r2, r3,   r2, r3, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],
          [s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, r3, r2,   r3, r2, r2, r3, r3,   r2, r2, r3, s2, s2,   s2, s2, s2, s2, s2,   s2, s2, s2, s2, s2,   s2,],

          [g2, g1, g1, g2, g2,   g2, g2, g3, g2, g2,   g2, g1, g2, g2, g2,   g2, g2, g2, g2, g1,   g2, g3, g2, g2, g2,   g2, g2, g2, g1, g2,   g3, g2, g2, g3, g2,   g2,],
          [g2, g2, g2, g3, g2,   g1, g2, g1, g2, g3,   g2, g2, g3, g2, g3,   g2, g3, g2, g2, g2,   g2, g3, g2, g1, g2,   g2, g3, g3, g2, g1,   g2, g2, g2, g1, g2,   g3,],
          [g2, g3, g2, g2, g2,   g2, g3, g2, g2, g2,   g3, g2, g2, g1, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g3, g2,   g2, g2, g2, g2, g3,   g3, g2, g2, g2, g2,   g1,],
          [e1, e1, e3, e2, e1,   e2, e1, e1, e1, e1,   e1, e2, e1, e3, e1,   e1, e1, e1, e1, e1,   e1, e1, e3, e1, e1,   e1, e2, e1, e1, e3,   e1, e1, e1, e2, e1,   e1,],
          [e3, e1, e1, e1, e2,   e1, e1, e3, e1, e3,   e1, e3, e1, e1, e1,   e1, e1, e1, e1, e1,   e1, e1, e2, e1, e1,   e2, e1, e1, e1, e1,   e1, e2, e1, e3, e1,   e1,],

          [e1, e1, e1, e3, e1,   e1, e2, e1, e1, e1,   e1, e1, e1, e2, e1,   e1, e1, e1, e1, e1,   e1, e2, e1, e1, e3,   e1, e1, e3, e1, e1,   e2, e1, e1, e2, e1,   e2,],
          [e1, e1, e1, e1, e1,   e2, e1, e1, e1, e2,   e1, e1, e1, e3, e1,   e1, e1, e1, e1, e1,   e1, e1, e3, e1, e1,   e1, e2, e1, e1, e1,   e3, e1, e2, e1, e1,   e1,],
          [e3, e1, e2, e3, e1,   e3, e1, e1, e1, e1,   e1, e1, e1, e1, e1,   e2, e1, e1, e1, e1,   e2, e1, e2, e1, e2,   e1, e1, e1, e2, e1,   e1, e2, e1, e1, e3,   e1,],
          [e1, e1, e1, e1, e1,   e1, e1, e1, e1, e1,   e1, e3, e1, e1, e2,   e1, e1, e1, e1, e1,   e1, e1, e1, e1, e2,   e1, e1, e3, e1, e1,   e2, e1, e2, e1, e1,   e1,],
          [g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2,],

          [g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2, g2, g2, g2, g2,   g2,],

        ]
        this.color_stard_for = {
          sky_up: "#ABDBE8", sky_down: "#D2E6ED",
          cloud: "#FFFFFF",
          grass_some: "#91BA51", grass_more: "#83AB38", grass_a_lot: "#5A7C2F",
          rock_little: "#DED3D9", rock_greate: "#9E8E99", rock_huge: "#80747E",
          earth_dry: "#6D6452", earth_moist: "#635846", earth_wet: "#585149"
        }
      }
      else if (to.path === '/roadmap') {
        const [e2,] = ['earth_moist',]
        this.resolution = this.square_length
        this.grid = [[e2,],]
        this.color_stard_for = {
          earth_moist: "#635846",
        }
      }
      else if (to.path === '/whitepaper') {
        const [s1,] = ['sky_up',]
        this.resolution = this.square_length
        this.grid = [[s1,],]
        this.color_stard_for = {
          sky_up: "#ABDBE8",
        }
      }

      try {
        this.P5_obj.remove()
      }catch (e){
        console.log(e)
      }
      this.P5_obj = new P5(this.sketch,to.path.toString().substr(1))
    }
  },
  created(){
    document.title = "｜賣花少年";
  },
})
</script>

<style scoped>
</style>