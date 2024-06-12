<template>
  <div
    class="nav-fixed"
    :class="showNav ? 'showNav' : 'hideNav'"
    :style="outstyle"
  >
    <button class="icon" @click="clickHome()"></button>
    <div class="links">
      <button
        class="links-item :hover"
        v-for="(item, i) in links"
        :key="i"
        @click="clickItem(item)"
      >
        {{ item.name }}
      </button>
    </div>
  </div>
  <!-- </div> -->
</template>

<script>
export default {
  name: "navigation",
  props: {
    outstyle: {
      type: String,
      default: ""
    }
  },
  data: () => {
    return {
      showNav: true,
      links: [
        {
          name: "Works",
          link: "https://sara-bai.webflow.io/#works"
        },
        // {
        //   name: "Sides",
        //   path: "/Sides"
        // },
        {
          name: "Resume",
          link:
            "https://drive.google.com/file/d/1XdsVh4PBOmFHXlIxaiYL0g5L1n9Ln3hy/view"
        }
      ],
      offset: 0,
      timer: null
    };
  },
  mounted() {
    window.addEventListener("scroll", this.scrollListener, true);

    this.timer = setInterval(() => {
      this.offset = this.scrollTop();
    }, 100);
  },
  destroyed() {
    window.removeEventListener("scroll", this.scrollListener);

    clearInterval(this.timer);
    this.timer = null;
  },
  computed: {
    active() {
      return this.$route.name;
    }
  },
  methods: {
    scrollListener() {
      var scroll = this.scrollTop() - this.offset;
      if (!this.showNav && scroll < 0) {
        this.showNav = true;
        //添加你想要的事件
      } else if (this.showNav && scroll > 0) {
        //添加你想要的事件
        this.showNav = false;
      }
    },
    clickHome() {
      window.location.href = "https://sara-bai.webflow.io";
    },
    clickItem(item) {
      if (item.path) {
        this.$router.push(item.name);
        return;
      }

      if (item.link) {
        window.location.href = item.link;
      }
    },
    scrollTop() {
      return (
        window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop
      );
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.nav-fixed {
  z-index: 999;
  // position: fixed;
  position: sticky;
  top: 10px;
  margin: 0 auto 0 auto;
  padding: 4px;
  box-sizing: border-box;
  width: 290px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  background-color: rgba($color: #ffffff, $alpha: 0.6);
  box-shadow: 2px 2px 8px 0px #0000001a;
  border-radius: 99px;

  .icon {
    position: relative;
    width: 45px;
    height: 40px;
    background-image: url("/assets/icons/logo.png");
    background-repeat: no-repeat;
    background-position: center;
    background-size: contain;
  }

  .links {
    position: relative;
    margin: 0 0 0 60px;
    height: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;

    &-item {
      margin: 4px;
      padding: 8px 12px;
      font-family: Rubik;
      font-size: 16px;
      font-weight: 400;
      text-align: center;
      border-radius: 99px;

      :hover {
        background-color: rgba($color: #d5cfd8, $alpha: 0.8);
      }
    }
  }
}

button:hover {
  animation: none;
  background-color: rgba($color: #d5cfd8, $alpha: 0.8);
}

.showNav {
  animation: 500ms ease-in-out 0s normal forwards 1 running fadeInDown;
}

.hideNav {
  animation: 500ms ease-in-out 0s normal forwards 1 running fadeOutUp;
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translate(0, -100%);
  }
  to {
    opacity: 1;
    transform: none;
  }
}

@keyframes fadeOutUp {
  from {
    opacity: 1;
    transform: none;
  }
  to {
    opacity: 0;
    transform: translate(0, -100%);
  }
}
</style>
