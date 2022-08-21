<template>
<div class="container">
  <h1>Comentários</h1>
  <hr />   
   <FormTodo v-on:add-todo="addComment"></FormTodo>   
  <hr/>          
  <div class="list-group">
    <p v-if="comments.length <= 0">Sem Comentarios...</p>
    <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
        <span class="coment__author">Autor: <strong>{{comment.name}}</strong></span>
        <p>{{ comment.message }}</p>
        <div>
            <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
        </div>
    </div>
  </div>                           
</div>
</template>

<script>
import FormTodo from './FormTodo.vue';

export default {
    data() {
        return {
            comments: [],
        };
    },
    methods: {
        removeComment(index) {
            this.comments.splice(index, 1);
        },
        addComment(comment){
            this.comments.push(comment)
        }
    },
    computed: {
        allComments() {
            return this.comments.map(comment => ({
                ...comment,
                name: comment.name.trim() === "" ? "Anônimo" : comment.name
            }));
        }
    },
    watch: {
        comments(val) {
            console.log("val", val);
        }
    },
    components: { FormTodo }
}
</script>