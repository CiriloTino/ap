<template>
  <section>
    <div class="btn-group">
      <input class="btn-search" type="text" placeholder="Buscar" v-model="input_search" @keyup="buscar"/>
      <button class="btn" @click="showModal">Nuevo usuario</button>
    </div>

    <Modal
      v-show="isModalVisible"
      @close="closeModal"
    />

    <div class="table">
    <table>
      <thead>
        <tr>
          <th>Opciones</th>
          <th>Nombre completo</th>
          <th>Nickname</th>
          <th>Tipo de usuario</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>[show] [edit] [destroy]</td>
          <td>{{ nombreCompleto( user ) }}</td>
          <td>{{ user.nickname }}</td>
          <td>{{ user.tipo_usuario }}</td>
        </tr>
      </tbody>
    </table>
    </div>
  </section>
</template>





<script>
import data from './data'
import Modal from './Create_user'

export default {
  name: 'Users',
  components:{
    Modal,
  },
  data () {
    return {
      input_search: '',
      users: [],
      isModalVisible: false,
    };
  },

  created() {
    this.users = data
  },

  methods: {
    showModal() {
        this.isModalVisible = true;
      },
    closeModal() {
        this.isModalVisible = false;
    },
    nombreCompleto( item ){
      return `${item.nombre} ${item.apellidos}`
    },
    buscar(){
      console.log(this.input_search)
      let found = this.users.filter( 
        //(item) => item.nombre.toLowerCase() == this.input_search.toLowerCase()
        (item) => item.nombre.toLowerCase().startsWith(this.input_search.toLowerCase())
      )
      if( found.length > 0 & this.input_search!="")
        this.users = found
      else
        this.users = data
    },
  }
}
</script>




<style>


.table{
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: #fafafa;
  margin: 1rem;
  padding: 1rem;
  display: flex;
}

th{

font-family: Roboto;
font-style: normal;
font-weight: normal;
font-size: 1em;
line-height: 1em;
align-items: center;
color: #1B4698;
padding: 10px;
padding-right: 7em;
text-align: left;
border-bottom:2px solid #1B4698;
}

td{
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 1em;
  line-height: 1em;
  align-items: center;
  text-align: left;
  color: #6D798F;
  padding: 10px;
  border-bottom:1px solid #1B4698;
}


.btn-search{
width: 46em;
background: #FFFFFF;
border: 1px solid #B7C3D9;
box-sizing: border-box;
padding:1em;
margin-right: 5rem;
}

.btn{
  background: #011843;
  color: white;
  padding:1em;
  padding-left:2em;
  padding-right:2em;
}

.btn-group{
  justify-content: center;
  align-items: center;
  text-align: center;
}

</style>