<script setup lang="ts">
import { reactive } from 'vue';
import TextInput from './components/TextInput.vue';

const textOutput = reactive({
  boxWhite: "box with white area",
  boxGrey: "box with grey area",
  circleWhite: "circle with white area",
  circleGrey: "circle with grey area",
  free: "free area",
});
const coor = reactive({ x: '0', y: '0', text: '' });
const shapeCoor = reactive({
  rect: [
    [5, 15],
    [25, 15],
    [5, 5],
    [25, 5],
  ],
  round: [
    [25, 15],
    10,
  ],
});

const find = () => {
  const x = parseInt(coor.x);
  const y = parseInt(coor.y);

  if (x < 5 || x > 30) {
    coor.text = textOutput.free;
  }

  else if (
    x >= 5 && x < 20 && y >= 5 && y <= 15
    || x >= 20 && x <= 25 && y >= 5 && y < 10
  ) {
    coor.text = textOutput.boxWhite;
  }

  else if (x >= 20 && x <= 25 && y >= 10 && y <= 15) {
    const roundX = (shapeCoor.round[0] as number[])[0];
    const roundY = (shapeCoor.round[0] as number[])[1];
    const radius = shapeCoor.round[1] as number;
    const dx = Math.abs(x - roundX);
    const dy = Math.abs(y - roundY);
    const num = ((dx * 2) + (dy * 2));

    if (num <= radius) {
      coor.text = textOutput.circleGrey;
    }
    else {
      coor.text = textOutput.boxWhite;
    }
  }

  else {
    const roundX = (shapeCoor.round[0] as number[])[0];
    const roundY = (shapeCoor.round[0] as number[])[1];
    const radius = shapeCoor.round[1] as number;
    const dx = Math.abs(x - roundX);
    const dy = Math.abs(y - roundY);
    const num = ((dx * 2) + (dy * 2));

    console.log(dx, dy);
    console.log((num <= (radius) && num >= 0) || num <= -10);

    if ((num <= (radius) && num >= 0) || num <= -10) {
      coor.text = textOutput.circleWhite;
    }
    else {
      coor.text = textOutput.free;
    }
  }
};
</script>

<template>
  <div id="container">
    <div class="card">
      <img src="./../public/image.png">
      <TextInput @enter="find" type="number" v-model="coor.x" label="x" />
      <TextInput @enter="find" type="number" v-model="coor.y" label="y" class="mt-s" />
      <div>
        <button @click="find">submit</button>
      </div>
      <div class="mt-s">
        {{ coor.text }}
      </div>
    </div>
  </div>
</template>

<style scoped>
#container {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.card {
  border: 1px solid rgb(80, 80, 80);
  border-radius: 0.5rem;
  padding: 1rem;

}

mt-s {
  margin-top: 1rem;
}
</style>
