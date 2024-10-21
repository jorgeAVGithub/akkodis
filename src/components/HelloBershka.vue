<template>
  <section class="categories-block">
    <h3>Categories</h3>
    <div class="json-formatter">
      {{ JSON.stringify(categories, null, 2) }}
    </div>
    <div>
      <input v-model="categoryToFind" type="text" placeholder="Search category" />
      <button @click="findCategoryPath">Find Path</button>
    </div>
    <div v-if="categoryPath">
      <h4>Category Path:</h4>
      <p>{{ categoryPath }}</p>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HelloBershka',
  data() {
    return {
      categories: [
        {
          name: 'category1',
          subcategories: [
            {
              name: 'category2',
              subcategories: []
            },
            {
              name: 'category3',
              subcategories: [
                {
                  name: 'category4',
                  subcategories: []
                }
              ]
            }
          ]
        },
        {
          name: 'category5',
          subcategories: []
        }
      ],
      categoryToFind: "",
      categoryPath: ""
    };
  },
  methods: {
    
    getCategoryPath(categories, categoryName) {
      for (let category of categories) {
        if (category.name === categoryName) {
          return `/${category.name}`;
        }
        if (category.subcategories.length) {
          const subcategoryPath = this.getCategoryPath(category.subcategories, categoryName);
          if (subcategoryPath) {
            return `/${category.name}${subcategoryPath}`;
          }
        }
      }
      return null;
    },
    
    findCategoryPath() {
      if (this.categoryToFind.trim()) {
        const path = this.getCategoryPath(this.categories, this.categoryToFind.trim());
        if (path) {
          this.categoryPath = path;
        } else {
          this.categoryPath = `Please enter a category name.`;
        }
      } else {
        alert("Please enter a category name.");
      }
    }
  }
}

</script>

<style scoped>
.categories-block{
  display: flex;
  flex-direction: column;
  align-items: center;
}
h3 {
  margin: 40px 0 0;
}
.json-formatter{
  margin: 10px 0;
  white-space: pre-wrap;
  font-family: monospace;
}
</style>
