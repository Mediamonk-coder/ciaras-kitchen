<template>
  <div class="w-full">
    <div class="m-auto max-w-5xl mt-10">
      <!-- <h1 class="text-3xl text-orange-700 font-semibold mx-5 my-5">
        {{ recipe.title.toUpperCase() }}
      </h1> -->
      <div class="md:flex md:content-start">
        <div>
          <div
            class="rounded-lg overflow-hidden object-cover max-w-md h-56 mx-5"
          >
            <img
              v-if="recipe.imageUrl !== null"
              :src="recipe.imageUrl"
              :alt="recipe.title"
            />
            <img
              v-else
              src="../static/images/feast4x3.png"
              :alt="recipe.title"
            />
          </div>
          <h1 class="text-3xl text-orange-700 font-semibold mx-5 my-5">
            {{ recipe.title.toUpperCase() }}
          </h1>
        </div>

        <div class="items-start">
          <div
            class="rounded border-2 border-solid border-gray-200 px-5 py-2 my-5 md:my-0 mx-5 max-w-2xl"
          >
            <h1 class="title-text text-xl font-semibold">INGREDIENTS:</h1>
            <ul>
              <li
                v-for="ingredient in recipe.ingredients"
                :key="ingredient.name"
                class="flex item-end"
              >
                <h6 class="font-bold">
                  {{ ingredient.amount }} {{ ingredient.unit }}
                </h6>
                <h6 class="ml-2">{{ ingredient.name }}</h6>
              </li>
            </ul>
          </div>
        </div>
      </div>
      <section
        class="rounded border-2 border-solid border-gray-200 px-5 py-2 my-5 mx-5 max-w-4xl"
      >
        <h1 class="title-text text-xl font-semibold">STEPS:</h1>
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

<style scoped>
.title-text {
  color: #5f9ea0;
}
</style>
