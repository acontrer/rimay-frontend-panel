  <template><div>
    <nav class="navbar navbar-default">
      <div class="container">
        <div class="container-fluid">
        <ul class="nav navbar-nav ">
        <li><a v-link="'secretquote'"  @click="account()" v-if="user.authenticated">Mis Datos</a></li>
          <li><a v-link="'login'" @click="login()"  v-if="!user.authenticated">Login</a></li>
          <li><a v-link="'secretquote'"  @click="admin()" v-if="user.data.Usuario_tipos_id=='1'">Usuarios</a></li>

          
          <li><a v-link="'secretquote'"  @click="dashboard()" v-if="user.data.Usuario_tipos_id=='1'">Panel Gráfico</a></li>
          <li><a v-link="'secretquote'"  @click="dialog()" v-if="user.data.Usuario_tipos_id=='1'">Panel de Diálogo</a></li>
          <li><a v-link="'secretquote'"  @click="files()" v-if="user.data.Usuario_tipos_id=='1'">Archivos</a></li>
          <li><a v-link="'login'" v-if="user.authenticated" @click="logout()">Salir</a></li>
        </ul>
      </div>
      </div>    
    </nav>
    <div class="container">
      <router-view></router-view>
    </div>
    </div>
  </template>

  <script>
  import auth from './auth'
  export default {
    data() {
      return {
        user: auth.user
      }
    },
    methods: {

      login() {
        this.$router.push('/login')
      },

      logout() {
        auth.logout()
        this.$router.push('/login')
      },

      admin() {
       this.$router.push('/admin')
      },
      dashboard() {
       this.$router.push('/dashboard')
      },
      dialog() {
       this.$router.push('/dialog')
      },
      files() {
       this.$router.push('/files')
      },
     account() {
       this.$router.push('/account')
      }
    }
  }
  </script>