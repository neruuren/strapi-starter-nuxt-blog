<template>
  <div>

    <Categories :categories="categories"></Categories>

  </div>
</template>

<script>
import categoriesQuery from '~/apollo/queries/category/categories'
import Categories from '~/components/Categories'

export default {
  data() {
    return {
      articles: [],
    }
  },
  components: {
    Categories
  },
  apollo: {
    categories: {
      prefetch: true,
      query: categoriesQuery,
      variables () {
        return { id: parseInt(this.$route.params.id) }
      }
    }
  }
}
</script>
