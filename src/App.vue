<template>
  <div class="app" id="app" ref="app">
     <loading
        :active="isLoading"
        :can-cancel="true"
        :on-cancel="onCancel"
        :is-full-page="fullPage"
      />
    <header class="header" v-show="!isLoading">
      <div class="icons">
        <div class="socials">
          <a href="https://discord.gg/kBhJcKJb6q" target="_blank"
            ><img src="./assets/discord.svg" alt="discord"
          /></a>
          <a href="https://twitter.com/NearzooNFT" target="_blank"
            ><img src="./assets/twitter.svg" alt="twitter"
          /></a>
        <button class="wallet">Connect wallet</button>
        </div>
      </div>
      <div class="logo">
        <span>Easy</span>
        <span>bears</span>
      </div>
      <div class="roadmap">
        <span>roadmap</span>
        <span>whitepaper</span>
        <button class="wallet">Connect wallet</button>
      </div>
    </header>
    <img class="app-img" src="./assets/photo.jpg" alt="" ref="img" />
    <ul class="text1" v-show="!isLoading">
      <li>Discord / Twtiter Marketing</li>
      <li>Genesis collection mint</li>
      <li>Magic Eden Listing</li>
      <li>Holders verification system</li>
    </ul>
    <ul class="text2" v-show="!isLoading">
      <li>Lending protocol development</li>
      <li>Merch launch</li>
      <li>DAO treasury and voting launch</li>
    </ul>
    <ul class="text3" v-show="!isLoading">
      <li>Website 2.0 release</li>
      <li>NFT futures system development</li>
      <li>Community wallet launch</li>
      <li>NFT Index development</li>
    </ul>
    <ul class="text4" v-show="!isLoading">
      <li>Real life community building</li>
      <li>NFT Trading ecosystem launch</li>
      <li>Building more Dapps on Solana ecosystem</li>
    </ul>
    <p class="addText">Ease Bears</p>
    <img
      src="./assets/arrow.svg"
      class="arrowLeft"
      alt="left"
      @keypress.left="leftScroll"
      @click="leftScroll"
    />
    <img
      src="./assets/arrow.svg"
      class="arrowRight"
      alt="right"
      @keypress.left="rightScroll"
      @click="rightScroll"
    />
  </div>
</template>

<script>
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.css';
import smoothscroll from 'smoothscroll-polyfill';

smoothscroll.polyfill();

export default {
  name: 'NearZoo',
  components: {
    Loading,
  },
  data: () => ({
    disableLeftScroll: false,
    mobileOpened: false,
    x: 0,
    isLoading: true,
  }),
  mounted() {
    setTimeout(() => {
      this.isLoading = false;
    }, 1000);
    window.addEventListener('wheel', this.onWheel);
    window.addEventListener('resize', this.applyStyle);

    setTimeout(() => {
      this.$refs.app.style.width = `${this.$refs.img.offsetWidth}px`;
    }, 100);
  },
  methods: {
    onWheel(event) {
      if (event.deltaX !== 0) {
        return;
      }

      this.x += event.deltaY > 0 ? 100 : -100;
      window.scroll(this.x, 0);
    },
    applyStyle() {
      this.$refs.app.style.width = `${this.$refs.img.offsetWidth}px`;
    },
    rightScroll() {
      const scroll = window.scrollX + 500;
      window.scroll(scroll, 0);
    },
    leftScroll() {
      const scroll = window.scrollX - 500;
      window.scroll(scroll, 0);
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap");

$maxWidthNumber: 1920;

@mixin adaptiv-font($pcSize, $mobSize) {
  $addSize: $pcSize - $mobSize;
  $addMobSize: $addSize + $addSize * 0.7;

  @media (max-width: 767px) {
    font-size: calc(
      #{$mobSize + px} + #{$addMobSize} * ((100vw - 320px) / #{$maxWidthNumber})
    );
  }

  @media (min-width: 767px) {
    font-size: calc(
      #{$mobSize + px} + #{$addSize} * (100vw / #{$maxWidthNumber})
    );
  }
}

* {
  margin: 0;
  padding: 0;
  font-family: "Montserrat", sans-serif;
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Chrome/Safari/Opera */
  -khtml-user-select: none; /* Konqueror */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none;
  scroll-behavior: smooth;

  ::-webkit-scrollbar {
    display: none;
  }
}

body {
  overflow-y: hidden;
}

.app {
  position: relative;
  height: 100vh;

  &-img {
    max-height: 100%;
  }
}

.wallet {
  text-transform: uppercase;
  font-size: 12px;
  font-weight: 600;
  color: white;
  height: 20px;
  background: rgba($color: #000000, $alpha: 0.4);
  border: none;
  outline: none;
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  border-radius: 4px;

  @media (max-width: 1000px) {
    display: none;
  }
}

.header {
  position: fixed;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 24px;
  width: 100vw;
  height: 60px;
  background: rgba($color: #000000, $alpha: 0.2);
  box-sizing: border-box;

  @media (max-width: 1000px) {
    padding: 0 10px;
  }

  .icons {
    display: flex;
    align-items: center;
  }

  .socials {
    display: flex;
    align-items: center;

    .wallet {
      margin-left: 12px;
      display: none;

      @media (max-width: 1000px) {
        display: flex;
        height: 30px;
      }
    }

    img {
      width: 20px;
      cursor: pointer;

      @media (max-width: 1000px) {
        width: 30px;
      }
    }

    img:last-child {
      margin-left: 15px;

      @media (max-width: 1000px) {
        margin-left: 15px;
      }
    }
  }

  .roadmap {
    display: flex;
    align-items: center;

    @media (max-width: 1000px) {
      flex-direction: column;
      justify-content: space-between;
      height: 70%;
    }

    span {
      font-weight: 14px;
      text-transform: uppercase;
      color: white;
      font-weight: 600;
      cursor: pointer;
      margin-right: 12px;

      @media (max-width: 1000px) {
        font-size: 12px;
      }
    }
  }
}

@-webkit-keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
}

.logo {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  transform: translate(-50%, -1px);
  left: 50%;

  @media (max-width: 1000px) {
    display: none;
  }

  span {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 24px;
    color: white;

    @media (max-width: 700px) {
      font-size: 14px;
    }
  }
}

p,
ul {
  position: absolute;
  font-weight: bold;
  list-style: none;
  line-height: 30px;
  @include adaptiv-font(16, 10);
}

li {
  position: relative;

  &::before {
    content: "";
    position: absolute;
    width: 10px;
    height: 10px;
    top: 10px;
    left: -12px;
    background: url("./assets/logo.svg");
  }
}

.text1 {
  right: 16.5%;
  top: 13%;
  @media (max-width: 767px) {
    right: 17.5%;
    top: 12%;
  }
}

.text4 {
  max-width: 250px;
  right: 2%;
  bottom: 10%;
  @media (max-width: 767px) {
    right: 2%;
    bottom: 12%;
  }
}

.text3 {
  right: 16.5%;
  bottom: 12%;
  @media (max-width: 767px) {
    right: 17%;
    bottom: 11%;
  }
}

.text2 {
  right: 3%;
  top: 15%;
  @media (max-width: 767px) {
    right: 4%;
    top: 15%;
  }
}

.addText {
  font-size: 24px;
  text-transform: uppercase;
  font-weight: 600;
  bottom: 20%;
  left: 40.5%;
}

.arrowLeft {
  position: fixed;
  left: 5%;
  top: 50%;
  width: 40px;
  transform: rotate(180deg);
  cursor: pointer;
}

.arrowRight {
  position: fixed;
  right: 5%;
  top: 50%;
  width: 40px;
  cursor: pointer;
}

@media (max-width: 600px) {
  .arrowLeft,
  .arrowRight {
    display: none;
  }
}

// .mobile-header {
//   display: none;
// }

// .burger {
//   width: 25px;
//   height: 3px;
//   background: white;
//   position: fixed;
//   left: 10%;
//   top: 8%;

//   &::after, &::before {
//     width: 25px;
//     height: 3px;
//     position: fixed;
//     background: white;
//     left: 10%;
//     top: 9%;
//     content: '';
//   }

//   &::before {
//     top: 7%;
//   }
// }

// .mobile-menu {
//   width: 100vw;
//   height: 100vh;
//   background: white;
//   z-index: 2;

//   & .cross {
//     width: 15px;
//     height: 2px;
//     background: #000000;
//     position: fixed;
//     top: 9%;
//     left: 10%;
//     transform: ;
//     &::after {

//     }
//   }
// }

// @media (max-width: 1000px) {
//   .header {
//     display: none;
//   }

//   .mobile-header {
//     display: block;
//   }
// }
</style>
