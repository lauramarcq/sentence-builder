<template>
  <div class="max-w-sm rounded overflow-hidden shadow-lg">
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">The Coldest Sunset</div>
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
    <div>{{ returnedSentence }}</div>
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
      subject,
      verb,
      object,
      options,
      handleSubmit,
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
