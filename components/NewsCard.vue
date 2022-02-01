<template>
    <div class="card">
        <v-card>
            <NuxtLink :to="'news/'+article.id"><v-img :src="article.preview_image"></v-img></NuxtLink>
            <NuxtLink :to="'news/'+article.id" class="link"><v-card-title>{{ article.name }}</v-card-title></NuxtLink>
            <v-card-text>{{ article.shortDesc }}</v-card-text>
            <v-card-text>
                <v-row>
                    <v-col>Date: {{ article.date }}</v-col>
                    <v-col>category: {{ article.category }}</v-col>
                </v-row>
            </v-card-text>            
        </v-card>          
    </div>
</template>
<script>
export default {
    props:{
        article:{
            type: Object,
            required: true,
        }
    }
}
</script>
<style scoped>
.link{
    color: white;
    text-decoration: none;
}
.card{
    transition-duration: .4s;
}
.card:hover{
    transform: rotate(4deg);
    transition-duration: .4s;
}
</style>