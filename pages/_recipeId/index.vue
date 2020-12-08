<template>
  <div>
    <RecipeTemplate :recipe="recipe" />
  </div>
</template>

<script>
import axios from 'axios'
import RecipeTemplate from '../../components/Recipe'

export default {
  components: { RecipeTemplate },
  // eslint-disable-next-line no-unused-vars
  async asyncData(context) {
    try {
      let snapshot = await axios.get(
        `https://us-central1-recipe-app-c7160.cloudfunctions.net/getRecipes/${context.params.recipeId}`
      )
      console.log(snapshot)
      let recipe = { id: snapshot.id, ...snapshot.data }
      console.log(recipe)
      return { recipe }
    } catch (e) {
      console.log(e)
    }
  },
}
</script>
