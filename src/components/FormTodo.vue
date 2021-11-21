<template>
    <div class="form-todo form-group">
        <p>
            <input v-model="id" placeholder="id" type="text" name="author" class="form-control" hidden="true">
        </p>
        <p>
            <input v-model="name" placeholder="nome" type="text" name="author" class="form-control">
        </p>
        <p>
            <input v-model="email" required placeholder="email" type="text" name="email" class="form-control">
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
            id: 0,
            name:'',
            email:'',
            message: '',
        }
    },
    methods: {
        addComment(){
            //validando para não ir campo vazio this.name.trim() === '' ||
            if( this.message.trim() && this.email.trim() === ''){
                return;
            }

            //emitindo para todos elementos que estiverem ouvindo
            this.$emit('add-todo', {
                id: this.id,
                name: this.name,
                email: this.email,
                message: this.message,
            });

            //apaga após comentar
            this.name= '';
            this.email= '';
            this.message='';
        },

    
    }

}
</script>