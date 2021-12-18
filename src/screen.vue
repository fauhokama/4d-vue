<script>
export default /* #__PURE__*/ {
  name: "Screen",
  props: {
    down: {
      type: Object,
      default: () => {},
    },
    up: {
      type: Object,
      default: () => {},
    },
    left: {
      type: Object,
      default: () => {},
    },
    right: {
      type: Object,
      default: () => {},
    },
    time: {
      type: Number,
      default: 300,
    },
  },
  data() {
    return {
      screen: null,
      halfTime: this.time / 2,
    };
  },
  mounted() {
    this.screen = document.getElementById("screen");
    this.screen.style.animation = "fade-in ease-out 100ms";
    window.addEventListener("keydown", this.doCommand);
  },
  destroyed() {
    window.removeEventListener("keydown", this.doCommand);
  },
  methods: {
    doCommand(e) {
      switch (e.key) {
        case "ArrowUp":
          this.move("up");
          break;
        case "ArrowDown":
          this.move("down");
          break;
        case "ArrowLeft":
          this.move("left");
          break;
        case "ArrowRight":
          this.move("right");
          break;
      }
    },
    move(direction) {
      if (this[direction]) {
        document.body.style.transition = `background-color ${this.time}ms`;
        document.body.style.backgroundColor = this[direction].bgColor;
        // eslint-disable-next-line max-len
        this.screen.style.animation = `${direction} ease-out ${this.time}ms, fade-out ease-out ${this.halfTime}ms`;
        this.screen.style.animationFillMode = "both";
        setTimeout(() => {
          this.$router.push(this[direction].path);
        }, this.time);
      }
    },
  },
};
</script>

<template>
  <div id="screen">
    <slot />
  </div>
</template>

<style>
#screen {
  overflow: hidden;
  width: 100vw;
  height: 100vh;
}

@keyframes right {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(100%);
  }
}

@keyframes left {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-100%);
  }
}

@keyframes down {
  from {
    transform: translatey(0);
  }
  to {
    transform: translateY(100%);
  }
}

@keyframes up {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(-100%);
  }
}

@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes fade-out {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
</style>
