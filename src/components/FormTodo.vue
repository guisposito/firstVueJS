<template>
    <div class="form-todo form-group">
        <p>
            <input v-model="name" placeholder="nome" type="text" name="author" class="form-control">
        </p>
        <p>
            <textarea v-model="message" name="message" placeholder="Comentário" class="form-control"></textarea>
        </p>
        <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
</template>

<script>
export default {
    data(){
        return{
            name:'',
            message: '',
        }
    },
    methods: {
        addComment(){
            //validando para não ir campo vazio this.name.trim() === '' ||
            if( this.message.trim() === ''){
                return;
            }

            //emitindo para todos elementos que estiverem ouvindo
            this.$emit('add-todo', {
                name: this.name,
                message: this.message,
            });

            //apaga após comentar
            this.name= '';
            this.message='';
        },
    }

}
</script>