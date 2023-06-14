## 效果图

<ClientOnly><doFirstTime></doFirstTime></ClientOnly>

## 代码

```vue
<template>
  <div style="position: relative;">
    <div class="but" @click="convertedFunc">
      {{ count }} click and i will do the first time
    </div>
    <div ref="shader" class="shader"></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
const count = ref(0);
const shader = ref(null);
let deg = ref(0);
const doFirstTimeFunc = (func, time = 2000) => {
  let t = true;
  let n = null;
  return () => {
    clearTimeout(n);
    if (t == true) {
      func();
      t = false;
    }
    n = setTimeout(() => {
      t = true;
    }, time);
  };
};
const doClick = () => {
  count.value++;
};
let convertedFunc = null;
onMounted(() => {
  animation = () => {
    if (deg.value < 360 && shader.value) {
      deg.value += 1;
      shader.value.style.background = `conic-gradient(from ${deg.value}deg, #7460ba, #fff 5deg 340deg, #7857ed)`;
    } else deg.value = 0;
    requestAnimationFrame(animation);
  };
  convertedFunc = doFirstTimeFunc(doClick);
  animation();
});
let animation = null;
</script>

<style scoped>
.but {
  display: flex;
  justify-content: center;
  position: relative;
  width: 280px;
  height: 30px;
  font-weight: bolder;
  background-color: black;
  color: white;
  border-radius: 1em;
  cursor: pointer;
}

.but:hover {
  background-color: white;
  color: black;
}

.shader {
  position: absolute;
  top: -2px;
  left: -2px;
  height: 34px;
  width: 284px;
  border-radius: 1em;
  z-index: -1;
}
</style>

<style>
.theme-default-content {
  position: absolute;
  z-index: -2;
}
</style>
```