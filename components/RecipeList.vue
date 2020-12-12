<template>
  <section>
    <div
      v-for="recipe in recipeList"
      :key="recipe.id"
      class="mx-auto bg-white overflow-hidden max-w-xl md:max-w-3xl my-5"
    >
      <hr />
      <nuxt-link :to="'/' + recipe.id">
        <div class="flex pt-3">
          <div>
            <div class="object-contain w-40">
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
          </div>
          <ul>
            <h1 class="px-6 font-bold text-2xl mb-2 recipe-title">
              {{ recipe.title }}
            </h1>
            <div class="px-6 w-100">
              <hr />
              <div class="font-light tracking-wider mt-1">
                by {{ recipe.creatorName.toUpperCase() }}
              </div>
            </div>
          </ul>
        </div>
      </nuxt-link>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    // eslint-disable-next-line vue/require-prop-types
    recipeList: {
      required: true,
    },
  },
}
</script>

<style scoped>
.recipe-title {
  color: maroon;
}
</style>
