<template>
<v-container>
    <v-carousel
    cycle
    height="500"
    hide-delimiter-background
    show-arrows-on-hover
  >
    <v-carousel-item
      v-for="(slide, i) in slides"
      :key="i"
      :src="slide.preview_image"
    >
    <v-row
        class="fill-height"
        align="center"
        justify="center"
    >
        <div class="text-h2">
         <NuxtLink :to="'news/'+slide.id" class="link">{{ slide.name }}</NuxtLink>
        </div>
    </v-row>
    </v-carousel-item>
  </v-carousel>
  <v-row class="mt-16">
      <v-col v-for="(article, i) in articles" :key="i">
          <news-card v-bind:article="article"></news-card>
      </v-col>
  </v-row>
</v-container>

</template>
<script>
  export default {
    data () {
      return {
        slides: [],
        articles: [],
      }
    },
    methods:{
        async fetchAllNews(){
            const articles = await this.$axios.$get('http://demo-api.vsdev.space/api/articles')
            this.articles = articles;
            let categories = await this.$axios.$get('http://demo-api.vsdev.space/api/categories')
            categories = categories


            articles.forEach(article => {
                categories.forEach(category => {
                    if(article.category === category.id)
                        article.category = category.name
                })
            })
            this.slides = this.getSlides()
        },
        getSlides(){
            let slides = []
            this.articles.forEach(article => {

                if(article.slider){
                    slides.push(article)
                }
            });
            return slides
        },
    },
    mounted(){
        this.fetchAllNews();
    }
  }
</script>
<style scoped>
.link{
    color: white;
    text-decoration: none;
}
</style>