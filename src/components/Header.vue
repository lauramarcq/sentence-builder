<template>
  <header class="bg-white shadow">
    <div class="w-7xl px-4 py-6 sm:px-6 lg:px-8">
      <h1 class="text-3xl font-bold text-gray-900">Some kind of title</h1>
      <h3>Some kind of subtitle</h3>
    </div>
    <div class="explanation-container">
      <p>
        Make sentences and questions by putting the verbs in the right form!
      </p>
      <p class="example">(+) A bear <b>sleeps</b> all day in winter</p>
    </div>
  </header>
</template>

<script>
export default {
  name: "HeaderComponent",
};
</script>

<style scoped>
header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding-left: 4rem;
  padding-right: 2rem;
}
.explanation-container {
  padding: 0.2rem 1rem;
  border: 2px solid #f5c863;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: fit-content;
  align-self: center;
}

.explanation-container p {
  text-align: right;
  padding: 0 10px;
}
.explanation-container .example {
  color: grey;
}
</style>
