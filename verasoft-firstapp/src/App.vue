<template>
  <div id="app">
    <navbar></navbar>
    <div class="container">
          <button class="btn btn-success" 
          @click="isNew = !isNew">
            Create
          </button>
          <RecipeForm v-if="isNew" @saveRecipe="addRecipe"/>
          <input type="text" classs="form-control" 
             v-model="searchtext">
          <ul>
            <li v-for="(recipe,index) in filterList" :key="index+recipe.title">
              {{ recipe.title}}
            </li>
          </ul>
    </div>

  </div>
</template>
<script>
import Navbar from "./layout/navbar";
import RecipeForm from "./components/RecipeForm";

export default {
  name: "app",
  components: {
    Navbar,RecipeForm
  },
  data() {
    return {
      recipes: [],
      isNew: false,
      searchtext: ''
    }
  },
  mounted () {
    if (localStorage.getItem('recipes')) {
      this.recipes = JSON.parse(localStorage.getItem('recipes'))
    }
  },
  computed: {
    filterList() {
      return this.recipes.filter(recipe => {
        return recipe.title.toLowerCase().indexOf(this.searchtext.toLowerCase()) > -1
      })
    }
  },
  methods: {
    setLocalStorage() {
      localStorage.setItem('recipes', JSON.stringify(this.recipes))
    },
    addRecipe (recipe) {
      this.recipes.push(recipe)
      this.setLocalStorage()
      this.isNew = false
    },
    searchRecipe() {
      return this.recipes.filter((recipe) => {
        return recipe.title.toLowerCase().indexOf(this.searchtext.toLowerCase()) > -1
      })
    }
  },
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
