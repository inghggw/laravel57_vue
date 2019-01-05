<template>
   <div class="row justify-content-center">
        <div class="col-md-8">

            <formulario-component @newPensamiento="addPensamiento">
            </formulario-component>
            
            <pensamiento-component v-for="(dPensamiento,index) in pensamientos" 
                :key="dPensamiento.id" 
                :pensamiento="dPensamiento"
                @delete="deletePensamiento(index)"
                @update="updatePensamiento(index,dPensamiento)">
            </pensamiento-component>

        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                pensamientos:[]
            }
        },
        mounted() {
            console.log('Component MiPensamiento mounted.')
            axios.get('/pensamiento')
                    .then((r)=>{
                        this.pensamientos = r.data;
                    })
        },
        methods:{
            addPensamiento(d){
                this.pensamientos.push(d);
            },
            deletePensamiento(index){
                this.pensamientos.splice(index,1);
            },
            updatePensamiento(index,d){
                this.pensamientos[index]=d;
            }
        }
    }
</script>
