<template>
  <svg height="500" width="500" viewBox="0 0 500 500">
    <circle id="clock-frame"/>
    <circle id="clock-background"/>
    <component v-for="m in 60" :key="m" :is="m % 5 ? 'rect' : 'circle'" class="mark rotate" :style="{ '--rotate': deg(6 * m) }"/>
    <rect id="second" class="rotate" :style="{ '--rotate': deg(6 * second) }"/>
    <rect id="minute" class="rotate" :style="{ '--rotate': deg(6 * minute) }"/>
    <rect id="hour" class="rotate" :style="{ '--rotate': deg(30 * hour) }"/>
    <circle id="clock-pin"/>
  </svg>
</template>

<script>
  export default {
    name: 'Clock',
    data () {
      return this.getDate()
    },
    mounted () {
      window.setInterval(() => {
        const { hour, minute, second } = this.getDate()
        this.hour = hour
        this.minute = minute
        this.second = second
      }, 1000)
    },
    methods: {
      deg (n) {
        return `${n}deg`
      },
      getDate () {
        const date = new Date()
        return {
          hour: date.getHours(),
          minute: date.getMinutes(),
          second: date.getSeconds()
        }
      }
    }
  }
</script>

<style lang="scss">
  $color_black: #222;

  .rotate {
    transform: rotate(var(--rotate, 0deg));
    transform-origin: 50%;
  }

  @mixin rectangle ($color, $height, $width, $x, $y){
    fill: $color;
    height: $height;
    width: $width;
    x: $x;
    y: $y;
  }

  @mixin circle ($color, $cx, $cy, $radius) {
    fill: $color;
    cx: $cx;
    cy: $cy;
    r: $radius;
  }

  #hour {
    @include rectangle($color_black, 120px, 10px, 245px, 130px);
  }

  #minute {
    @include rectangle($color_black, 160px, 10px, 245px, 90px);
  }

  #second {
    @include rectangle(crimson, 160px, 4px, 248px, 90px);
  }

  circle.mark {
    @include circle(#ccc, 250px, 75px, 5px);
  }

  rect.mark {
    @include rectangle(#ddd, 10px, 2px, 249px, 70px);
  }

  #clock-frame {
    @include circle($color_black, 250px, 250px, 250px);
  }

  #clock-background {
    @include circle(#f7f7f7, 250px, 250px, 200px);
  }

  #clock-pin {
    @include circle($color_black, 250px, 250px, 15px);
  }
</style>