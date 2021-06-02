<template>

  <section class="src-components-tabla-datos justify-context-center">
    <div class="jumbotron">
      <h2>2. Http request</h2>
      <hr>
      <div class="text-center">
        <button class="btn btn-outline-primary m-3 mb-4" @click="getDatosXML()">Pedir XMLHttpRequest</button>
         <button class="btn btn-outline-success m-3 mb-4" @click="getDatosFetch()">Pedir FETCH</button>
         <button class="btn btn-outline-warning m-3 mb-4" @click="getDatosAxios()">Pedir AXIOS</button> 
      </div>
      <div class="text-center">
        <button class="btn btn-outline-secondary m-2 mb-4" @click="resetDatos()">Resetear</button>
      </div>
      <div v-if="datos.length" class="table-responsive">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th v-for="(col,index) in getCols" :key="index">{{ col }}</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(dato, index) in datos" :key="index">
              <td v-for="(col,index) in getCols" :key="index">{{dato[col]}}</td>
            </tr>
          </tbody>
        </table>

        <div class="alert alert-secondary">Se encontraron {{ datos.length }} datos</div>
      </div>
      <div v-else class="alert alert-danger">No se encontraron datos</div>
    </div>
  </section>

</template>

<script lang="js">

// import TablaHttp from './TablaHttp.vue';

  export default  {
    name: 'src-components-tabla-datos',
    // components: {
    //   TablaHttp
    // },
    props: [],
    mounted () {

    },
    data () {
      return {
        url: 'https://609dbeea33eed800179570ad.mockapi.io/usuarios',
        datos: []
      }
    },
    methods: {

      getDatosXML() {
        let xhr = new XMLHttpRequest()
        xhr.open('get', this.url)
        xhr.addEventListener('load', () => {
          if(xhr.status == 200) {
            let respuesta = JSON.parse(xhr.response)
            console.log('XMLHttpRequest', respuesta)
            this.datos = respuesta
          }
          else {
            console.error(`Error en GET -> status: ${xhr.status}`)
          }
        })
        xhr.addEventListener('error', e => {
          console.error(`Error XMLHttpRequest ->`, e)
        })
        xhr.send()
      },

      getDatosFetch() {
        fetch(this.url)
        .then(datos => datos.json())
        .then(respuesta => {
          console.log('FETCH', respuesta)
          this.datos = respuesta
        })
        .catch(error => console.log(error))

      },

      getDatosAxios() {
        this.axios(this.url)
        .then(respuesta => {
          console.log('AXIOS', respuesta.data)
          this.datos = respuesta.data
        })
        .catch(error => console.error(error))
      },

      resetDatos() {
        this.datos = []
      }

    },
    computed: {
      getCols() {
        return Object.keys(this.datos[0])
      }

    }
}


</script>

<style scoped lang="css">
  .src-components-tabla-datos {

  }
</style>
