<template>
  <div class="max-w-m rounded overflow-hidden shadow-lg">
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">Sentence Builder</div>
      <p class="text-gray-700 text-base">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus
        quia, nulla! Maiores et perferendis eaque, exercitationem praesentium
        nihil.
      </p>
    </div>
    <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="subject">
          Subject
        </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="subject"
          type="text"
          placeholder="girl"
          v-model="subject"
        />
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="verb">
          Verb
        </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="verb"
          type="text"
          placeholder="read"
          v-model="verb"
        />
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="object">
          Object
        </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="object"
          type="text"
          placeholder="book"
          v-model="object"
        />
        <p class="text-red-500 text-xs italic">{{ validationError }}</p>
      </div>
      <div class="flex items-center justify-between">
        <button
          class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
          type="button"
        >
          Cancel
        </button>
        <button
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
          type="submit"
          @click="handleSubmit"
        >
          Submit
        </button>
      </div>
    </form>
    <div v-if="returnedSentence">
      <button
        class="bg-green-500 hover:bg-gray-700 text-black font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        type="button"
        v-if="revealAnswer || answerCheck === 'Correct!'"
        @click="revealAnswer = false"
      >
        {{ returnedSentence }} (click here to hide the answer)
      </button>
      <div v-else-if="returnedSentence">
        <button
          class="bg-yellow-500 hover:bg-gray-700 text-black font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
          type="button"
          @click="revealAnswer = true"
        >
          Answer hiding under here...it will be revealed once you get the answer
          correct! (or click here to reveal it now)
        </button>
      </div>
      <div class="mb-6 px-6 py-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="answer">
          Type your answer here
        </label>
        <textarea
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="answer"
          type="text"
          placeholder="write a sentence that makes sense with the words you provided above."
          v-model="answer"
          @input="handleAnswer"
        />
        <p
          class="text-red-500 text-xs italic"
          v-if="answer && answerCheck === 'Incorrect!'"
        >
          {{ answerCheck }}
        </p>
        <p
          class="text-green-500 text-s italic"
          v-if="answer && answerCheck === 'Correct!'"
        >
          {{ answerCheck }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
import axios from "axios";

export default {
  name: "CardInput",
  setup() {
    // Your setup logic here
    let validationError = ref("");
    let returnedSentence = ref("");
    let answerCheck = ref("");
    let answer = ref("");
    const revealAnswer = ref(false);
    const subject = ref("");
    const verb = ref("");
    const object = ref("");

    const options = reactive({
      method: "GET",
      url: "https://linguatools-sentence-generating.p.rapidapi.com/realise",
      params: {
        object: object,
        subject: subject,
        verb: verb,
      },
      headers: {
        "X-RapidAPI-Key": "5c774a765fmsh5df914e934fece7p1b3364jsneb69d7ce4f23",
        "X-RapidAPI-Host": "linguatools-sentence-generating.p.rapidapi.com",
      },
    });

    function handleAnswer(event) {
      if (event.target.value === returnedSentence.value) {
        answerCheck.value = "Correct!";
      } else {
        answerCheck.value = "Incorrect!";
      }
    }

    async function handleSubmit(event) {
      event.preventDefault();
      try {
        const response = await axios.request(options);
        console.log("response", response.data);
        returnedSentence.value = response.data.sentence;

        console.log(response.data);
      } catch (error) {
        console.error(error);
        validationError.value = error.response.data.error_message;
      }
    }

    return {
      validationError,
      returnedSentence,
      answerCheck,
      revealAnswer,
      answer,
      subject,
      verb,
      object,
      options,
      handleSubmit,
      handleAnswer,
    };
  },
};
</script>

<style scoped>
/* Your component styles here */
/* .error-text-input {
  shadow appearance-none border border-red-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline
} */
</style>
