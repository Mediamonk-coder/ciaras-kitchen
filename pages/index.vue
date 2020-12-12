<template>
  <div class="w-full">
    <section class="sticky top-0">
      <section class="search">
        <div>
          <img
            v-if="searchType === 'Ingredients'"
            class="search-pic absolute z-0 w-full object-cover"
            src="../static/images/tomatoes.jpg"
            alt="background image"
          />
          <img
            v-else
            class="search-pic absolute z-0 w-full object-cover"
            src="../static/images/dish.jpg"
            alt="background image"
          />
        </div>
        <section
          v-if="searchType === 'Title'"
          class="search-title flex items-center z-10 h-48 justify-center max-w-lg m-auto"
        >
          <div class="count-icon ml-5 z-10">
            <h1 class="text-white font-bold text-center text-lg">
              {{ recipeCountTitle }}
            </h1>
          </div>
          <input
            v-model="searchTitle"
            type="text"
            class="flex w-full ml-2 mr-5 my-2 px-5 py-2 rounded border-solid border-2 border-gray-400 z-10"
            placeholder="search by name"
          />
        </section>
        <section
          v-else
          class="search-title flex items-center z-10 h-48 justify-center max-w-lg m-auto"
        >
          <div class="count-icon ml-5 z-10">
            <h1 class="text-white font-bold text-center text-lg">
              {{ recipeCountIngredient }}
            </h1>
          </div>
          <input
            v-model="searchIngredient"
            type="text"
            class="flex w-full ml-2 mr-5 my-2 px-5 py-2 rounded border-solid border-2 border-gray-400 z-10"
            placeholder="search by ingredients"
          />
        </section>
      </section>
      <div class="search-toggle mx-5 text-right z-10">
        <button
          v-if="searchType === 'Title'"
          class="border hover:bg-gray-600 shadow px-4 pt-3 pb-1 text-white rounded-b-xl"
          @click="toggleSearch"
        >
          search by ingredient
        </button>
        <button
          v-else
          class="border hover:bg-gray-600 shadow px-4 pt-3 pb-1 text-white rounded-b-xl"
          @click="toggleSearch"
        >
          search by name
        </button>
      </div>
    </section>
    <section>
      <RecipeList
        v-if="searchTitle !== ''"
        :recipe-list="filteredRecipesByTitle"
      ></RecipeList>
      <RecipeList
        v-else
        :recipe-list="filteredRecipesByIngredient"
      ></RecipeList>
    </section>
  </div>
</template>
<script>
import axios from 'axios'
import RecipeList from '../components/RecipeList'

export default {
  components: { RecipeList },
  // eslint-disable-next-line no-unused-vars
  async asyncData(context) {
    try {
      let res = await axios.get(
        'https://us-central1-recipe-app-c7160.cloudfunctions.net/getRecipes'
      )
      let recipes = res.data
      recipes.sort((a, b) => a.title.localeCompare(b.title.toUpperCase()))
      //console.log(recipes[0])
      return { recipes }
    } catch (e) {
      console.log(e)
    }
  },

  data() {
    return {
      searchTitle: '',
      searchIngredient: '',
      searchType: 'Title',
    }
  },

  computed: {
    recipeCountTitle() {
      return this.filteredRecipesByTitle.length
    },

    recipeCountIngredient() {
      return this.filteredRecipesByIngredient.size
    },

    filteredRecipesByTitle() {
      return this.recipes.filter((recipe) => {
        return recipe.title.toLowerCase().match(this.searchTitle.toLowerCase())
      })
    },

    filteredRecipesByIngredient() {
      let filteredList = []
      this.recipes.forEach((recipe) => {
        let recipeIngredients = []
        recipe.ingredients.forEach((ingredient) => {
          recipeIngredients.push(ingredient.name.toLowerCase())
        })
        console.log(recipeIngredients)
        recipeIngredients.forEach((ingredient) => {
          if (ingredient.match(this.searchIngredient.toLowerCase())) {
            filteredList.push(recipe)
          }
        })
        // if (recipeIngredients.includes(this.search.toLowerCase())) {
        //   filteredList.push(recipe)
        // }
      })
      let setFilteredList = new Set(filteredList)
      return setFilteredList
    },
  },

  methods: {
    toggleSearch() {
      if (this.searchType === 'Title') {
        this.searchType = 'Ingredients'
      } else {
        this.searchType = 'Title'
      }
      this.searchTitle = ''
      this.searchIngredient = ''
    },
  },
}
</script>

<style scoped>
.count-icon {
  border-radius: 50%;
  width: 38px;
  height: 38px;
  padding: 10px;
  background: maroon;
  display: flex;
  align-items: center;
  justify-content: center;
}
.search-pic {
  height: 200px;
}

button {
  outline: none;
  background: maroon;
}
</style>
