<template>
    <div>

    <button v-if="show" @click.prevent="unsave()" class="btn btn-success">Unsave Job</button>
    <button v-else @click.prevent="save()" class="btn btn-dark">Save Job</button>


    </div>
</template>

<script>
    export default {
        props:['jobid','faborited'],

        data(){
            return{
                show:true
            }
        },
        mounted() {
           this.show= this.jobFavorited ? true:false
        },
        computed:{
          jobFavorited(){
              this.faborited
          }
        },
        methods:{
            save(){
              axios.post('/save/'+this.jobid)
                  .then(response=>this.show=true)
                  .catch(error=>alert('Error'))
            },
            unsave(){
                axios.post('/unsave/'+this.jobid)
                    .then(response=>this.show=false)
                    .catch(error=>alert('Error'))
            },
        }

    }
</script>
