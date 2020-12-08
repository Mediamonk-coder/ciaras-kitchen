<template>
  <div>
    <input
      v-model="search"
      type="text"
      class="rounded border-solid border-2 border-gray-400 w-full max-w-3xl mx-5 my-2 px-5 py-2 overflow-hidden"
      placeholder="search recipes"
    />
    <h2>{{ recipeCount }}</h2>
    <div
      v-for="recipe in filteredRecipes"
      :key="recipe.id"
      class="max-w-sm mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl mx-5 my-5"
    >
      <nuxt-link :to="'/' + recipe.id">
        <div class="md:flex">
          <div>
            <div class="md:object-contain sm:object-cover md:w-40">
              <img
                v-if="recipe.imageUrl !== null"
                :src="recipe.imageUrl"
                :alt="recipe.title"
              />
              <img
                v-else
                src="../assets/images/feast4x3.png"
                :alt="recipe.title"
              />
            </div>
          </div>
          <div class="px-6 py-4 font-bold text-xl mb-2">{{ recipe.title }}</div>
        </div>
      </nuxt-link>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  // eslint-disable-next-line no-unused-vars
  async asyncData(context) {
    try {
      let res = await axios.get(
        'https://us-central1-recipe-app-c7160.cloudfunctions.net/getRecipes'
      )
      let recipes = res.data
      recipes.sort((a, b) => a.title.localeCompare(b.title.toUpperCase()))
      console.log(recipes[0])
      return { recipes }
    } catch (e) {
      console.log(e)
    }
  },

  data() {
    return {
      search: '',
    }
  },

  computed: {
    recipeCount() {
      return this.recipes.length
    },
    filteredRecipes() {
      return this.recipes.filter((recipe) => {
        return recipe.title.toLowerCase().match(this.search.toLowerCase())
      })
    },
  },
}
</script>
