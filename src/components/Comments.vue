<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr/>
        <FormTodo v-on:add-todo="addComment"></FormTodo>
        <hr/>
        <div class="list-group">
            <p v-if="comments.length <=0">Sem Comentários...</p>
            <div class="list-group-item" v-for="(comment, index) in allComments" :key="comment.id">
                <span class="comment_author">Autor: <strong>{{ comment.name }}</strong></span>
                <p>{{ comment.message }}</p>
                <div>
                    <button class="btn btn-success btn-sm" style="margin: 2.5px;" v-on:click.prevent="" title="Excluir">Editar</button>
                    <button class="btn btn-danger btn-sm" style="margin: 2.5px;" v-on:click.prevent="removeComment(index)" title="Excluir">Excluir</button>
                </div>
            </div>
        </div>
        <hr/>
    </div>
</template>

<script>
//importando o formulário
import FormTodo from './FormTodo.vue';
export default{
    components:{
        FormTodo
    },
    //função que retorna um objeto disponiveis para usar dentro do template
    data(){
        return{
            comments: [],
        }
    },
    //todos os metodos disponibilizados para o template pelas diretivas
    methods: {
        addComment(comment){
            this.comments.push(comment);
        },
        removeComment(index){
            //removendo o item do array
            this.comments.splice(index, 1);
            
        }

    },
    //relacionado a parte de visualização
    computed:{
        allComments(){
            //pegando toda lista de comentários
            return this.comments.map(comment =>({
                ...comment,
                // todo nome que for string vazia irá printar o anonimo
                name: comment.name.trim() === '' ? 'Anônimo' : comment.name
            }))
        }
    },
    //monitora qualquer ação dentro de algo
    watch: {
        comments(val){
            console.log('val', val);
        }
    }
}

</script>