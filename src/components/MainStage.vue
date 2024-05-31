<template>
  <div class="stage-container">
    <div class="button-area">
      <button
        @click="triggerClick = !triggerClick"
        type="button"
        class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      >
        Start!
      </button>
      <div class="stack-buttons">
        <button
          type="button"
          class="inline-flex items-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
        >
          Flip Stack 1
        </button>
        <button
          type="button"
          class="inline-flex items-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
        >
          Flip Stack 2
        </button>
        <button
          type="button"
          class="inline-flex items-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
        >
          Flip Stack 3
        </button>
      </div>
      <div class="dice-area">Dice</div>
    </div>
    <div class="card-area">
      <div class="subject-cards">
        <SingleCard
          class="subject"
          v-for="(card, i) in subjectContent"
          :key="i"
          :cardContent="subjectContent[i]"
          :inputId="`subject${i}`"
          :labelId="`subject${i}`"
          :triggerClick="triggerClick"
        ></SingleCard>
      </div>
      <div class="verb-cards">
        <SingleCard
          class="verb"
          v-for="(card, i) in verbContent"
          :key="i"
          :cardContent="verbContent[i]"
          :inputId="`verb${i}`"
          :labelId="`verb${i}`"
          :triggerClick="triggerClick"
        ></SingleCard>
      </div>
      <div class="object-cards">
        <SingleCard
          class="object"
          v-for="(card, i) in objectContent"
          :key="i"
          :cardContent="objectContent[i]"
          :inputId="`object${i}`"
          :labelId="`object${i}`"
          :triggerClick="triggerClick"
        ></SingleCard>
      </div>
    </div>
  </div>
</template>

<script>
import SingleCard from "./SingleCard.vue";
import { reactive, ref } from "vue";

export default {
  name: "MainStage",
  components: {
    SingleCard,
  },
  setup() {
    let subjectContent = reactive(["The subject", "A subject", "Some subject"]);
    let verbContent = reactive(["has", "will have", "could have"]);
    let objectContent = reactive(["an object", "the object", "some object"]);
    let triggerClick = ref(false);

    return {
      subjectContent,
      verbContent,
      objectContent,
      triggerClick,
    };
  },
};
</script>

<style scoped>
.stage-container {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  height: 100vh;
}

.button-area {
  min-width: 30%;
  height: 100%;
  margin-top: 20%;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.stack-buttons {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.card-area {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  height: 100%;
  min-width: 70%;
}

.subject-cards,
.verb-cards,
.object-cards {
  position: relative;
  top: 0;
  left: 0;
}

.subject-cards .subject {
  position: absolute;
}
.verb-cards .verb {
  position: absolute;
}

.object-cards .object {
  position: absolute;
}
</style>
