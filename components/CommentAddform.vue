<template>
<div class="addComment">
    <v-row>
        <v-col>
            <form @submit.prevent>
                <v-text-field
                v-model="comment.user_name"
                label="Name"
                ></v-text-field>
                <text-input
                v-bind:modelValue="comment.comment"
                    v-model="comment.comment"
                    @CommentInput="Oninput"
                ></text-input>
                <v-btn
                class="mr-4"
                @click="submit"
                >
                submit
                </v-btn>
                <v-btn @click="clear">
                clear
                </v-btn>
            </form>
        </v-col>
    </v-row>    
</div>    
</template>

<script>

export default {
    data(){
        return {
            comment:{
                user_name: '',
                comment: '',
            }
        }
    },
    methods:{
        submit(){
            this.$emit('createComment', this.comment)
        },
        clear(){
            this.comment.user_name = ''
            this.comment.comment = ''
        },
        Oninput(textComment){
            this.comment.comment = textComment
        }
    }
}
</script>
