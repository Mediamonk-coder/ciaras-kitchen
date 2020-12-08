<template>
  <div class="w-full">
    <h1 class="text-3xl text-orange-700 font-semibold flex w-full mx-5 my-5">
      {{ recipe.title.toUpperCase() }}
    </h1>
    <div class="flex">
      <div class="rounded-lg overflow-hidden object-cover max-w-md mx-5">
        <img
          v-if="recipe.imageUrl !== null"
          :src="recipe.imageUrl"
          :alt="recipe.title"
        />
        <img v-else src="../assets/images/feast4x3.png" :alt="recipe.title" />
      </div>
      <div class="content-spacearound">
        <div
          class="border-solid rounded-xl border-gray-200 border-2 p-2 w-full"
        >
          <h1 class="text-xl font-medium text-blue-400">Ingredients:</h1>
          <ul>
            <li v-for="ingredient in recipe.ingredients" :key="ingredient.name">
              {{ ingredient.name }}
            </li>
          </ul>
        </div>
      </div>
    </div>
    <section
      class="rounded border-2 border-solid border-gray-200 px-5 py-2 my-5 mx-5"
    >
      <h1 class="text-gray-500 text-xl font-semibold">STEPS:</h1>
      <ul>
        <div
          v-for="step in recipe.steps"
          :key="step"
          class="my-4 auto-cols-min"
        >
          <p class="inline mr-3">🥄</p>
          <p class="inline text-md">{{ step }}</p>
        </div>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  props: {
    recipe: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style scoped></style>
