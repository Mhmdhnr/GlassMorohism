<template>
  <div class="glass-container flex">
    <div v-for="n in bgCount" :id="`s${n}`" class="bg-square glass"></div>
    <slot />
  </div>
</template>

<script>
    export default {
        name: "GlassBG",
        props:['bgCount', 'bgRangeMin', 'bgRangeMax', 'bgDurationRange'],
        mounted() {
            for(let i = 1; i <= this.bgCount; i++) {
                let random = this.getRandom(this.bgRangeMin, this.bgRangeMax);
                let element = document.getElementById("s" + i);
                element.style.width = random + "px";
                element.style.height = random + "px";
                this.randomPosition(element)
            }
        },
        methods: {
            getRandom(min, max){
                return Math.floor(Math.random() * (max - min)) + min
            },
            randomPosition(element) {
                let baseTop = this.getRandom(10, 90);
                let baseLeft = this.getRandom(10, 100);
                element.style.transform = `rotate(${this.getRandom(-180, +180)}deg)`;
                element.style.top = baseTop + "%";
                element.style.left = baseLeft + "%";
                this.randomAnimation(element);
            },
            randomAnimation(element) {
                let currentDuration = this.getRandom(10000, this.bgDurationRange);
                element.style.transition = `all ${currentDuration}ms ease-in-out`;
                element.style.transform = `rotate(${this.getRandom(-180, +180)}deg) translateX(${this.getRandom(-300, 300)}%) translateY(${this.getRandom(-300, 300)}%)`;
                let _this = this;
                setInterval(function () {
                    element.style.transform = `rotate(${_this.getRandom(-180, +180)}deg) translateX(${_this.getRandom(-300, 300)}%) translateY(${_this.getRandom(-300, 300)}%)`;
                }, currentDuration)
            }
        }
    }
</script>

<style lang="scss" scoped>
  .glass-container {
    position: relative;
    display: flex;
    justify-content: center;
    @include gradient(90deg, #004056, #760089);
    background-position: center;
    width: 100vw;
    /*height: 90vh;*/
    height: auto;
    overflow: hidden;
    background-size: 200% 200%;
    -webkit-animation: bg-animation 15s ease infinite;
    .bg-square {
      position: absolute;
      border-radius: 10%;
      transition: all step-end;
      @include gradient(90deg, #11b77e, #17beac);
      @include shadow-light;
    }
  }

</style>
