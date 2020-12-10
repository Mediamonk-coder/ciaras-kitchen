<template>
  <section>
    <div
      v-for="recipe in recipeList"
      :key="recipe.id"
      class="mx-auto bg-white rounded-xl shadow-md overflow-hidden max-w-xl md:max-w-3xl my-5"
    >
      <nuxt-link :to="'/' + recipe.id">
        <div class="flex">
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
          <div class="px-6 py-4 font-bold text-xl mb-2 recipe-title">
            {{ recipe.title }}
          </div>
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
  color: #528b8b;
}
</style>
