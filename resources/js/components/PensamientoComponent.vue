<template>
    <div class="card mt-4">
        <div class="card-header">Publicado en {{pensamiento.created_at}} - Última actualización {{pensamiento.updated_at}}</div>

        <div class="card-body">
            <input v-if="editMode" type="text" class="form-control" v-model="pensamiento.descripcion">
            <p v-else>{{pensamiento.descripcion}}</p>
        </div>

        <div class="card-footer">
            <button v-if="editMode" class="btn btn-success" v-on:click="updateP()">Guardar</button>
            <button v-else class="btn btn-default" v-on:click="editP()">Editar</button>
            <button class="btn btn-danger" v-on:click="deleteP()">Eliminar</button>
        </div>
    </div>
</template>

<script>
    export default {
        props:['pensamiento'],
        data(){
            return{
                editMode:false
            }
        },
        mounted() {
            console.log('Component Pensamiento mounted.')
        },
        methods:{
            deleteP(){
                 axios.delete('/pensamiento/'+this.pensamiento.id)
                        .then(()=>{
                            this.$emit('delete');
                        });                
            },
            editP(){
                this.editMode = true;
            },
            updateP(){
                const d = {
                    descripcion:this.pensamiento.descripcion
                }
                axios.put('/pensamiento/'+this.pensamiento.id,d)
                        .then((r)=>{
                            this.editMode = false;                            
                            this.$emit('update',r.data);
                        });
                //this.$emit('update',this.pensamiento);
            }
        }
    }
</script>
