<template>
    <div class="card">
        <div class="card-header">¿En qué estás pensando?</div>

        <div class="card-body">
            <form action="" v-on:submit.prevent="createPensamiento()">
                <div class="form-group">
                    <label for="pensamiento">Ahora estoy pensando en:</label>
                    <input type="text" class="form-control" name="pensamiento" v-model="iDescripcion">
                </div>
                <button type="submit" class="btn btn-primary">Publicar pensamiento</button>
            </form>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                iDescripcion:'',
                i:2
            }
        },
        mounted() {
            console.log('Component Formulario mounted.')            
        },
        methods:{
            createPensamiento(){
                //alert(this.iDescripcion);
                let d = {
                    'id':this.i++,
                    'descripcion':this.iDescripcion,
                    'created_at':'30/12/2018'
                }
                this.$emit('newPensamiento',d);
                this.iDescripcion = '';
            }
        }
    }
</script>
