<template>
  <transition name="fade">
    <div v-if="show" class="preloader">
      <div class="preloader-content">
        <div class="logo">
          <img src="@/assets/Group-3.png" alt="" />
        </div>
      </div>
      <div class="circles">
        <div class="circle"></div>
        <div class="circle"></div>
        <div class="circle"></div>
        <div class="circle"></div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "preloader",
  data() {
    return {
      show: true,
    };
  },

  mounted() {
    this.showToggle();
  },
  methods: {
    //setting the animation to delay to let application load
    showToggle() {
      setTimeout(() => {
        this.show = false;
      }, 1000);
    },
  },
};
</script>

<style>
.preloader {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #112240 !important;
  z-index: 9999;
}

.preloader-content {
  display: flex;
  position: relative;
  flex-direction: column;
  background-color: rgba(0, 207, 253, 1);
  box-shadow: -1px 10px 25px -1px #0d6e84;
  padding: 1.5rem;
  height: 150px;
  width: 150px;
  border-radius: 40px;
  box-sizing: border-box;
}

.logo img {
  margin: -0.4rem;
  width: 120px;
  height: 120px;
  background: url(../assets/Group-3.png);
  background-repeat: no-repeat;
  animation-name: turnThis;
  animation-duration: 1s;
  transform: turn(0);
}

.circles {
  display: flex;
  margin: 1rem;
}

.circle {
  vertical-align: middle;
  top: 80px;
  width: 22px;
  height: 22px;
  margin: 0.5rem;
  background-color: #ffff;
  border-radius: 50%;
}

.circle {
  animation-name: scaleIn;
  animation-duration: 1s;
  transform: scale(0);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}

.logo {
  animation-name: scaleOut;
  animation-duration: 0.8s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
@keyframes turnThis {
  0% {
    transform: rotate(1turn);
  }
}

@keyframes scaleOut {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}

@keyframes scaleIn {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
</style>