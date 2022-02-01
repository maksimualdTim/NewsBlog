<template>
    <v-container>
        <v-row class="mt-8 mb-16">
            <v-col>
                <v-img :src="`../${article.preview_image}`" height="400" class="mb-8"></v-img>
                <div> {{ category }}</div>
                <div>{{ article.date }}</div>
            </v-col>
        </v-row>
        <v-row>
            <v-col><div class="title">{{ article.name }}</div></v-col>
        </v-row>
        <v-row>
            <v-col>{{ article.desc }}</v-col>
        </v-row>
        <article-comments v-bind:comments="comments" @send="submit"></article-comments>        
    </v-container>
</template>
<script>

export default{ 

    data(){
        return{
            article: {},
            category: '',
            comments: [],
            name: '',
            commentBody: '',
        }
        
    },
    methods:{
        async fetchArticleInfo(){
            const article = await this.$axios.$get('http://demo-api.vsdev.space/api/articles/' + this.$route.params.id);
            this.article = article;
            let categories = await this.$axios.get('http://demo-api.vsdev.space/api/categories')
            categories = categories.data
            
            categories.forEach(category => {
                if(category.id === article.category)
                    this.category = category.name
            });
        },
        async fetchComments(){
            const comments = await this.$axios.get(`http://demo-api.vsdev.space/api/articles/${this.$route.params.id}/comments`);
            this.comments = comments.data
        }, 
      submit (comment) {
          this.$axios.post(`http://demo-api.vsdev.space/api/articles/${this.$route.params.id}/comments`, comment)
          comment.created_at = new Date()
          this.comments.push(comment)
      },                 
    },
    mounted(){
        this.fetchArticleInfo();
        this.fetchComments();
    },  
}
</script>
<style scoped>
.title{
   text-align:center;
}
.comments{
    text-align: center;
}
</style>