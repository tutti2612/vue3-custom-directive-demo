<template>
  <div>
    <h1>Custom Directive Demo</h1>

    <div>
      <input v-focus:arg.hoge.fuga="'test'" />
    </div>

    <div>
      <input type="range" min="0" max="500" v-model="pinPadding" />
      <p v-pin:[direction]="pinPadding">
        Stick me {{ pinPadding + "px" }} from the {{ direction }} of the page
      </p>
    </div>

    <div>
      <div v-demo="{ color: 'white', text: 'hello!' }"></div>
    </div>

    <div>
      <MyComponent v-demo2="true" />
    </div>
  </div>
</template>

<script>
import MyComponent from "./components/MyComponent";

export default {
  components: {
    MyComponent,
  },
  data() {
    return {
      direction: "right",
      pinPadding: 200,
    };
  },
  directives: {
    // pin: {
    //   mounted(el, binding) {
    //     el.style.position = "fixed";
    //     const s = binding.arg || "top";
    //     el.style[s] = binding.value + "px";
    //   },
    //   updated(el, binding) {
    //     const s = binding.arg || "top";
    //     el.style[s] = binding.value + "px";
    //   },
    // },

    // mountedとupdatedに同じ処理を行うだけで良いのなら、アロー関数を使って短く書ける
    pin: (el, binding) => {
      el.style.position = "fixed";
      const s = binding.arg || "top";
      el.style[s] = binding.value + "px";
    },
    demo: (el, binding) => {
      console.log("demo:", binding.value.color); // => "white"
      console.log("demo:", binding.value.text); // => "hello!"
    },
    demo2: (el, binding) => {
      console.log("demo2:", el);
      console.log("demo2:", binding);
    },
    focus: {
      created() {
        console.log("custom-directive: created");
      },
      beforeMount() {
        console.log("custom-directive: beforeMount");
      },
      mounted(el, binding, vNode, prevNode) {
        console.log("custom-directive: mounted");
        console.log("el:", el);
        console.log("binding:", binding);
        console.log("vNode:", vNode);
        console.log("prevNode:", prevNode);
        el.focus();
      },
      beforeUpdate() {
        console.log("custom-directive: beforeUpdate");
      },
      updated() {
        console.log("custom-directive: updated");
      },
      beforeUnmount() {
        console.log("custom-directive: beforeUnmount");
      },
      unmounted() {
        console.log("custom-directive: unmounted");
      },
    },
  },
  created() {
    console.log("life-cycle: created");
  },
  beforeMount() {
    console.log("life-cycle: beforeMounted");
  },
  mounted() {
    console.log("life-cycle: mounted");
  },
  beforeUpdate() {
    console.log("life-cycle: beforeUpdate");
  },
  updated() {
    console.log("life-cycle: updated");
  },
  beforeUnmount() {
    console.log("life-cycle: beforeUnmount");
  },
  unmounted() {
    console.log("life-cycle: unmounted");
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
