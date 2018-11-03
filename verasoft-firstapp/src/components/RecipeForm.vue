<template>
    <div>
        <form @submit.prevent="" class="">
        <fieldset>

        <!-- Form Name -->
        <legend>Recipe FOrm</legend>
        <!-- Text input-->
        <div class="form-group row">
        <label class=" col-md-4 col-lg-4 control-label" for="title">Title</label>  
        <div class=" col-md-4 col-lg-8">
            <input id="title" name="title" v-model="recipe.title" type="text" placeholder="" class="form-control input-md">
            
        </div>
        </div>

        <!-- Text input-->
        <div class="form-group row">
        <label class=" col-md-4 col-lg-4 control-label" for="image_url">Image URL</label>  
        <div class=" col-md-4 col-lg-8">
        <input id="image_url" name="image_url" v-model="recipe.image_url" type="text" placeholder="" class="form-control input-md">
            
        </div>
        </div>

       <!-- Text input-->
        <div class="form-group row">
        <label class=" col-md-4 col-lg-4 control-label" for="description">Description</label>  
        <div class=" col-md-4 col-lg-8">
        <input id="description" name="description" v-model="recipe.description" type="text" placeholder="" class="form-control input-md">
            
        </div>
        </div>

        <div class="row">
            <div class="col">
            <button class="btn btn-primary float-right" @click="addIngredient">
                <i class="fa fa-plus-circle"></i> more Ingredient
            </button>
            </div>
        </div>

        <!-- Text input-->
        <div class="form-group row">
            <label class=" col-md-4 col-lg-4 control-label" for="ingredient">Ingredient</label>  
            <div class=" col-md-4 col-lg-8">
                <div v-for="(ingredient,index) in recipe.ingredient" 
                :key="index" >
                    <input v-model="recipe.ingredient[index]" 
                    type="text" class="form-control input-md">
                </div>
            </div>
        </div>

 

        <!-- Button (Double) -->
        <div class="form-group">
        <label class=" col-md-4 col-lg-4 control-label" for="submit-btn"></label>
        <div class=" col-md-4 col-lg-8">
            <button id="cancel-btn" name="cancel-btn" 
            class="btn btn-danger">Cancel</button>
            <button id="submit-btn" name="submit-btn" 
            class="btn btn-success" @click="save">Submit</button>
        </div>
        </div>

        </fieldset>
        </form>

    </div>
</template>

<script>
export default {
    data() {
        return {
            recipe: {
                title: '',
                description: '',
                image_url: '',
                ingredient: ['']
            }
        }
    },
    methods: {
        addIngredient() {
            this.recipe.ingredient.push('')
        },
        save () {
            this.$emit('saveRecipe', this.recipe)
        }
    },
};
</script>

<style scoped>
</style>