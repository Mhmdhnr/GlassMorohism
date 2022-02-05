<template>
    <div class="theme-toggle flex" @click="switchTheme()">
      <div class="sun-moon flex">
        <div class="sun flex">
          <div class="sun-circle flex">
            <div class="sun-ray" v-for="n in this.rayCount">
              <div class="ray"></div>
            </div>
          </div>
        </div>
        <div class="moon flex">
          <div class="moon-arc">
            <div class="star-1 star"></div>
            <div class="star-2 star"></div>
            <div class="star-3 star"></div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
        name: "ThemeToggle",
        data() {
            return {
                rayCount: 12,
            }
        },
        mounted() {
            for(let i = 0; i < 12; i++) {
              let ray = document.getElementsByClassName("sun-ray")[i];
              ray.style.transform = `rotateZ(${360 / this.rayCount * i}deg)`;
            }
            if (this.$colorMode.preference === "dark") {
                this.revealMoon();
            } else {
                this.revealSun();
            }

        },
        methods: {
            switchTheme() {
                let sun = document.getElementsByClassName("sun")[0];
                let moon = document.getElementsByClassName("moon")[0];
                if(this.$colorMode.preference === "dark") {
                    this.hideMoon();
                    setTimeout(() => {
                        this.$colorMode.preference = "light";
                        sun.style.display = "none";
                        moon.style.display = "none";
                        setTimeout(() => {
                            this.revealSun();
                        }, 100);
                    }, 900);
                } else {
                    this.hideSun();
                    setTimeout(() => {
                        this.$colorMode.preference = "dark";
                        sun.style.display = "none";
                        moon.style.display = "none";
                        setTimeout(() => {
                            this.revealMoon();
                        }, 100);
                    }, 750);
                }
            },
            revealSun() {
                let sun = document.getElementsByClassName("sun")[0];
                sun.style.display = "unset";
                let moon = document.getElementsByClassName("moon")[0];
                moon.style.display = "none";
                let circle = document.getElementsByClassName("sun-circle")[0];
                circle.style.width = "100%";
                circle.style.height = "100%";
                sun.style.transform = "rotate(180deg)";
                let i = 1;
                let revealSunRayInterval = setInterval(()  => {
                    let ray = document.getElementsByClassName("ray")[i - 1];
                    ray.style.width = "8%";
                    ray.style.height = "12%";
                    if (i++ === 12) {
                        clearInterval(revealSunRayInterval);
                    }
                }, 50)
            },
            hideSun() {
                let sun = document.getElementsByClassName("sun")[0];
                sun.style.transform = "rotate(-180deg)";
                let i = 1;
                let _this = this;
                let hideSunRayInterval = setInterval(()  => {
                    let ray = document.getElementsByClassName("ray")[i - 1];
                    ray.style.width = "0";
                    ray.style.height = "0";
                    if (i++ === _this.rayCount) {
                        clearInterval(hideSunRayInterval);
                        sun.style.display = "none";
                        let moon = document.getElementsByClassName("moon")[0];
                        moon.style.display = "unset";
                    }
                }, 50);
                setTimeout(() => {
                    let circle = document.getElementsByClassName("sun-circle")[0];
                    circle.style.width = "0";
                    circle.style.height = "0";
                }, 30 * this.rayCount)
            },
            revealMoon() {
                let sun = document.getElementsByClassName("sun")[0];
                sun.style.display = "none";
                let moon = document.getElementsByClassName("moon")[0];
                moon.style.display = "unset";
                let moonArc = document.getElementsByClassName("moon-arc")[0];
                let rect = moonArc.offsetWidth;
                moonArc.style.boxShadow = `${-rect * 0.3}px ${rect * 0.3}px 0 ${rect * 0.05}px var(--bg-color)`;
                let _this = this;
                setTimeout(function () {
                    let i = 1;
                    let revealMoonRayInterval = setInterval(()  => {
                        let star = document.getElementsByClassName("star")[i - 1];
                        let random = _this.getRandom(20,25);
                        star.style.width = `${random}%`;
                        star.style.height = `${random}%`;
                        if (i++ === 3) {
                            clearInterval(revealMoonRayInterval);
                        }
                    }, 100)
                }, 300)
            },
            hideMoon() {
                let sun = document.getElementsByClassName("sun")[0];
                sun.style.display = "none";
                let moon = document.getElementsByClassName("moon")[0];
                moon.style.display = "unset";
                let i = 1;
                let hideMoonRayInterval = setInterval(()  => {
                    let star = document.getElementsByClassName("star")[i - 1];
                    star.style.width = `0`;
                    star.style.height = `0`;
                    if (i++ === 3) {
                        clearInterval(hideMoonRayInterval);
                    }
                }, 100);
                setTimeout(() => {
                    let moonArc = document.getElementsByClassName("moon-arc")[0];
                    let rect = moonArc.offsetWidth;
                    moonArc.style.boxShadow = `unset`;
                }, 450)
            },
            getRandom(min, max){
                return Math.floor(Math.random() * (max - min)) + min
            },
        }
    }
</script>

<style lang="scss" scoped>
  .theme-toggle {
    @include glass;
    position: fixed;
    justify-content: center;
    z-index: 100;
    left: 0;
    top: 0;
    width: 70px;
    height: 70px;
    background-color: $text-color;
    clip-path: circle(80% at 0 0);
    .sun-moon {
      position: absolute;
      justify-content: center;
      left: 5%;
      top: 10%;
      width: 50%;
      height: 50%;
      .sun {
        position: relative;
        transition: all 1000ms;
        width: 60%;
        height: 60%;
        justify-content: center;
        .sun-circle {
          transition: all 400ms;
          justify-self: center;
          margin: auto;
          width: 0;
          height: 0;
          border-radius: 50%;
          background-color: $bg-color;
          .sun-ray {
            position: absolute;
            display: flex;
            justify-content: center;
            width: 150%;
            height: 150%;
            left: -25%;
            top: -25%;
            .ray {
              transition: height 100ms;
              width: 0;
              height: 0;
              border-radius: 40%;
              background-color: $bg-color;
            }
          }
        }
      }
      .moon {
        position: relative;
        transform: translateX(30%) translateY(-30%);
        width: 70%;
        height: 70%;
        justify-content: center;
        .moon-arc {
          position: relative;
          transition: all 500ms;
          width: 100%;
          height: 100%;
          border-radius: 50%;
          background-color: $text-color;
          .star-1 {
            width: 0;
            height: 0;
            left: 42%;
            top: 60%;
          }
          .star-2 {
            width: 0;
            height: 0;
            left: 58%;
            top: 40%;
          }
          .star-3 {
            width: 0;
            height: 0;
            left: 28%;
            top: 30%;
          }
        }
      }

    }
  }
  .star {
    transition: all 400ms;
    position: absolute;
    clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
    background-color: $bg-color;
  }
</style>
