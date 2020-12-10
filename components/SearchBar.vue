<template>
  <section class="search-title flex items-center">
    <input
      v-model="searchTitle"
      type="text"
      class="flex w-full mx-5 my-2 px-5 py-2 rounded border-solid border-2 border-gray-400"
      placeholder="search by name"
    />
    <div class="count-icon mr-5">
      <h1 class="text-white font-bold text-center text-lg">
        {{ recipeCountTitle }}
      </h1>
    </div>
  </section>
</template>

<script>
export default {}
</script>

<style></style>
