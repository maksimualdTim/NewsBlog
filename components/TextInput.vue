<template>
    <div class="text__input">
        <input 
        type="text" 
        :value="modelValue" 
        name="comment" 
        placeholder="Comment's text" 
        class="custom__input" 
        @input="updateInput">
    </div>
</template>
<script>

export default {
    props:{
        modelValue: [String, Number]
    },
    methods:{
        updateInput(event){
            this.$emit('CommentInput', event.target.value)
        }
    }
}
</script>

<style scoped>
.custom__input{
    width: 100%;
    border-bottom: 2px solid white;
    padding: 15px;
    color: white;
}
::-webkit-input-placeholder { /* Chrome */
  color: red;
}
:-ms-input-placeholder { /* IE 10+ */
  color: red;
}
::-moz-placeholder { /* Firefox 19+ */
  color: red;
  opacity: 1;
}
:-moz-placeholder { /* Firefox 4 - 18 */
  color: red;
  opacity: 1;
}
</style>