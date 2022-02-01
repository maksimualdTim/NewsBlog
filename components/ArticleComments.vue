<template>
    <div class="comments">
        <v-row>
            <v-col><div class="title">Comments</div></v-col>
        </v-row>
        <comment-addform
            @createComment="sendComment"
        ></comment-addform>
        <v-row v-for="(comment, i) in comments" :key="i">
            <v-col>
                <div class="comments">
                    <div>Username: {{ comment.user_name }}</div>
                    <div>Comment: {{ comment.comment }}</div>
                    <div>Date: {{ comment.created_at }}</div>                    
                </div>
            </v-col>
        </v-row>     
    </div>   
</template>

<script>
export default {
    props:{
        comments:{
            type: Array,
            required: true,
        }
    },
    methods:{
        sendComment(comment){
            this.$emit('send', comment)
        },
    }
}
</script>
