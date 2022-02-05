<template>
  <div class="glass-content flex">
    <div v-for="n in 8" class="card flex flex-column">
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
  $card-height: 200px;
  $card-width: 250px;
  $name-height: 70px;
  $des-height: 120px;
  $avatar-radius: calc(#{$card-height} - #{$name-height} - 30px);

  .glass-content {
    flex-wrap: wrap;
    padding: 100px 0;
    transform-style: preserve-3d;
    perspective: 1000px;
    @include boxed;
  }
  .card {
    position: relative;
    justify-content: space-between;
    border-radius: 24px;
    border: 3px solid transparent;
    background-clip: padding-box;
    margin: 70px 10px;
    /*padding: 20px;*/
    width: $card-width;
    height: $card-height;
    @include shadow-light;
    transition: all 500ms $cubic-negative;
    overflow: hidden;
    @include glass;
    &:hover {
      height: calc(#{$card-height} + #{$des-height});
      margin-top: calc(-1 * (#{$des-height} / 2));
      .des {
        display: unset;
      }
    }
    .who {
      width: 100%;
      height: 100%;
      justify-content: space-between;
      .avatar {
        width: $avatar-radius;
        height: $avatar-radius;
        border-radius: 50%;
        border: 1px solid $primary-color;
        transition: all 400ms;
        transform-origin: center;
        margin: 10px;
        &:hover {
          width: calc(2 * #{$avatar-radius});
          height: calc(2 * #{$avatar-radius});
          margin: calc((#{$card-height + $des-height - $name-height} - (2 * #{$avatar-radius}) - 8px) / 2);
        }
      }
      .text-area {
        justify-content: space-evenly;
        justify-self: flex-end;
        width: 100%;
        height: $name-height;
        @include glass;
        padding: 10px 20px;
        border-radius: 0 0 24px 24px;
        .age {
          font-size: 0.7em;
        }
        .name {
          font-size: 0.8em;
        }
      }
    }
    .des {
      display: none;
      height: $des-height;
      font-size: 0.7em;
      text-align: left;
      direction: ltr;
      font-family: Ubuntu, sans-serif;
      padding: 10px 20px;
      overflow: scroll;
      &::-webkit-scrollbar {
        display: none;
      }
    }
  }
  span {
    color: $text-color!important;
  }
</style>
