<template>
<div class="container">
    <div class="row">
        <div class="col-xs-12 col-sm-6 col-md-6">
            <div class="well well-sm">
                <div class="row">
                    <div class="col-sm-6 col-md-4">
                        <img src="http://placehold.it/380x500" alt="" class="img-rounded img-responsive" />
                    </div>
                    <div class="col-sm-6 col-md-8">
                        <h4>{{user.data.First_name}} {{user.data.Last_name}}</h4>
                        
                        <small><cite title="San Francisco, USA">{{user.data.Usuario_tipo.Tipo}} <i class="glyphicon glyphicon-map-marker">
                        
                        </i></cite></small>
                        <p>
                            <i class="glyphicon glyphicon-envelope"></i>{{user.data.Mail}}
                            <br />
                            <i class="glyphicon glyphicon-globe"></i><a href="http://www.jquery2dotnet.com">www.jquery2dotnet.com</a>
                            <br />
                            <i class="glyphicon glyphicon-gift"></i>June 02, 1988</p>
                        <!-- Split button -->
                        <div class="btn-group">
                           
                            <button v-on:click="changeState()" type="button" class="btn btn-primary">
                                Cambiar Contraseña</button>
                  
       
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
<div  v-show="isShow" id="formpass">
  <div class="form-group">
    <label for="usr">Contraseña Actual:</label>
    <input type="text" class="form-control" ref="pass">
  </div>
 
  <div class="form-group">
  <label for="usr">Nueva Contraseña:</label>
   <input type="text" class="form-control" ref="newpass">
  </div>
 
  <div class="form-group">
    <label for="usr">Re-Ingrese Nueva Contraseña:</label>
  <input type="text" class="form-control" ref="renewpass">
  </div>

    <div class="btn-group">
                   <button v-on:click="savePass()" type="button" class="btn btn-primary">
                                Guardar Cambios</button>
                  
       
            </div>

</div>

</div>

</template>

<script>
import Vue from 'vue'
import axios from 'axios';
import auth from '../auth'
import config from '../../config/appconfig.js';
console.log(config.server)

export default {
  name: 'Account',

  data(){

      return {
        isShow:false,
        user: auth.user
      }  
    },

  methods: {
    changeState: function () {
   
      this.isShow=true;
   
      },
    savePass: function () {
   
        console.log("Salvando Password2");
        
        if(this.$refs.pass.value){

          if(this.$refs.newpass.value==this.$refs.renewpass.value){

                axios.put(config.server_api+"usuario/",{headers:token})
                      .then((user_data) => {

                        console.log("data USer:", user_data.data)
                        this.user.data=user_data.data;
                        localStorage.setItem('user_data',JSON.stringify(user_data.data))
                        this.user.authenticated = true

                        context.$router.push('/admin')
                        
                      })
                      .catch(e => {
                        context.error=e.response.data.message
                    })
          }
        }
        
   
      }
    },

  created() {
  
  }
}




</script>
<style>
body{padding-top:30px;}

.glyphicon {  margin-bottom: 10px;margin-right: 10px;}

small {
display: block;
line-height: 1.428571429;
color: #999;
}
</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->

