<template>

  <div class="hello" >
             <div class="alert alert-danger" v-if="error">
                <p>{{ error }}</p>
              </div>
            <div class="alert alert-success" v-if="success">
                <p>{{ success }}</p>
            </div>

  <div v-if="visibleForm">

    <div class="form-group">
      <label for="usr" >Nombre de la Emergencia:</label>
      <input type="text" class="form-control" ref="tipo" >
    </div>

    <div class="btn-group">
         <button v-on:click="saveEmergencie()" type="button" class="btn btn-primary" >
                      Agregar Tipo de Emergencia

         </button>
    </div>


  </div>

<v-dialog/>

  <div  v-on:click="showPost()" class="btn btn-default">Agregar</div> 
    <h1>Tipo de Emergencias</h1>
    <table  class="" >
        <th>Identificador</th>      
        <th>Nombre</th>
        <th>Editar</th>
        <th>Eliminar</th>

      <tr v-for="item , key in posts">      

        <td >{{ item.Id }}</td>      
        <td ><div v-if=!item.edit> {{ item.Tipo}}</div> 
              <input v-if=item.edit type="text"  class="form-control" ref=item.Id :value=item.Tipo> 
              </td>
        <td v-if=!item.edit v-on:click="editEmergencie(item)" ><div class="btn btn-warning"> Editar </div></td>

        <td v-if=item.edit  v-on:click="updateEmergencie(item)" ><div class="btn btn-success"> Guardar </div></td>
        <td v-if=item.edit  v-on:click="cancelEmergencie(item)" ><div class="btn btn-warning"> Cancelar </div></td>

        <td v-if=!item.edit v-on:click="deleteEmergencie(item.Id,key)" ><div class="btn btn-danger"> Eliminar </div></td>
             
    
      </tr>
    </table>
  
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios';
import auth from '../auth'
import config from '../../config/appconfig.js';
import VModal from 'vue-js-modal'

Vue.use(VModal, { dialog: true })
export default {
  name: 'Admin',

  data: () => ({
    visibleForm:false,
    posts: [],
    errors: []
  }),

  methods: {
  hide () {
    this.$modal.hide('hello-world');
  },
    deleteEmergencie: function (ss,key) {
          console.log(key)
      this.$modal.show('dialog', {
        title: 'Atención',
        text: 'Desea eliminar el tipo de emergencia?',
        buttons: [
          { title: 'Eliminar', handler: () => { 
              axios.delete(config.server_api+"emTipo/"+ss,
              {},
              {
                headers:{'content-type': 'application/json'}})
                .then(response => {
                  this.$modal.hide('dialog')
                  Vue.delete(this.posts,key)

                })
                .catch(e => {
                  console.log(e)
                  this.errors.push(e)
                }) 
          } },
          { title: 'Cancelar' }
       ]
      })

       
         
            
    },  

    showPost(){
      this.visibleForm=true;
      console.log("ola")
    },

    editEmergencie(item){
 
      item.edit=true;

    },

    cancelEmergencie(item){
      console.log(item.edit)
      item.edit=false;

    },

    updateEmergencie(item){

      console.log(this.$refs["item.Id"][0].value)
         axios.put(config.server_api+"emTipo/"+item.Id,{"Tipo":this.$refs["item.Id"][0].value})
                  .then((response) => {

                    this.success="Emergencie Type was modified"
                    // this.posts.push(response.data)
                  })
                  .catch(e => {
                    this.error=e.response.data.message
                })
    },
    saveEmergencie(item){

        axios.post(config.server_api+"emTipo/",{"Tipo":this.$refs.tipo.value})
                  .then((response) => {

                    this.success="Emergencie Type was created"
                    this.posts.push(response.data)
                  })
                  .catch(e => {
                    this.error=e.response.data.message
                })
    }
  },

  created() {
    axios.get(config.server_api+'emTipo/')
    .then(response => {
      var out=[]
      
      response.data.forEach(function(ob1){
       
        console.log(ob1)
        ob1.edit=false;
        out.push(ob1)

      })
      
      this.posts = out

    })
    .catch(e => {
      this.errors.push(e)
    })


  }

}
  

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

