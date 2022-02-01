<template>
  <div class="glass-content">
    <div v-for="n in 8" class="card">
      <div class="who flex flex-column">
        <img class="avatar" src="../assets/images/me.jpeg" alt="">
        <div class="text-area flex flex-column">
          <span class="age">Age 27</span>
          <span class="name">American Beauty</span>
        </div>
      </div>
      <!--          <hr>-->
      <div class="des">
            <span>Front-end developer and UI designer from 2015. <br>
              Live in Tehran. <br>
              Ready to associate with colleagues. <br>
            </span>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: "ProfileCard"
    }
</script>

<style lang="scss">
  .glass-content {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    width: 1080px;
    padding: 100px 0;
    /*z-index: 10;*/
  }
  .card {
    position: relative;
    display: flex;
    flex-direction: column;
    border-radius: 24px;
    border: 3px solid transparent;
    background-clip: padding-box;
    margin: 60px 10px;
    width: 250px;
    height: 180px;
    box-shadow: 0 4px 12px 0 rgba(40, 40, 40, 0.5);
    padding: 20px;
    transform-origin: top;
    transition: all 500ms cubic-bezier(.175, .885, .32, 1.2);
    overflow: hidden;
    @include glass;
  }
  .card:hover {
    height: 300px;
    margin-top: -60px;
  }
  .card:hover .des {
    display: unset;
  }
  .who{
    justify-content: center;
  }
  .text-area {
    width: calc(100% + 40px);
    backdrop-filter: blur(10px) saturate(90%) ;
    background-color: rgba(255, 255, 255, 0.05);
    padding: 10px 20px;
    border-radius: 0 0 24px 24px;
  }
  span {
    color: $bg-color;
  }
  .age {
    font-size: 0.7em;
  }
  .name {
    font-size: 0.8em;
  }
  .avatar {
    width: 80px;
    height: 80px;
    margin-bottom: 10px;
    border-radius: 50%;
    border: 1px solid black;
    transition: all 400ms ;
  }
  .avatar:hover {
    width: 180px;
    height: 180px;
  }
  hr {
    margin: 5px 0;
    width: 100%;
    border: 1px solid rgba(255, 255, 255, 0.2);
  }
  .des {
    font-size: 0.65em;
    text-align: left;
    direction: ltr;
    font-family: Ubuntu, sans-serif;
    margin: 20px auto;
    display: none;
  }
</style>
