<template>

  <span class="src-components-formulario">
    <div class="jumbotron">
      <h2>1. Formulario</h2>
      <hr>
      <vue-form :state="formState" @submit.prevent="enviar()">
        <validate tag="div">
          <label for="nombre" >Nombre</label>
          <input type="text" id="nombre" name="nombre" autocomplete="off" class="form-control" v-model.trim="formData.nombre" :minlength="nombreMinLength" :maxlength="nombreMaxLength" required no-espacios>
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="no-espacios" class="alert alert-danger mt-1">No se permiten espacios en el campo</div>
            <div slot="minlength" class="alert alert-danger mt-1">Este campo requiere al menos {{ nombreMinLength }} caracteres</div>
            <div v-if="formData.nombre.length == nombreMaxLength" class="alert alert-danger mt-1">Este campo debe tener como máximo {{ nombreMaxLength }} caracteres</div>
            
          </field-messages>

        </validate>

        <validate tag="div">
          <label for="edad" >Edad</label>
          <input type="number" id="edad" name="edad" autocomplete="off" class="form-control" v-model.number="formData.edad" required :min="edadMin" :max="edadMax">
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">La edad mínima es de {{edadMin}} años</div>
            <div slot="max" class="alert alert-danger mt-1">La edad máxima es de {{edadMax}} años</div>
          </field-messages>
        </validate>

        <validate tag="div">
          <label for="email" >Email</label>
          <input type="email" id="email" name="email" autocomplete="off" class="form-control" v-model.trim="formData.email" minlength="3" required>
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="email" class="alert alert-danger mt-1">Email invalido</div>
          </field-messages>
        </validate>

        <button class="btn btn-success mt-3 ml-3 mb-3" type="submit" :disabled="formState.$invalid" >Enviar</button>
      </vue-form>
      <br>
      <h2>Datos del formulario</h2> 
      <hr>
      <TablaDatos :nameToShow="formData.nombre" :ageToShow="formData.edad" :emailToShow="formData.email" />

      
    </div>
  </span>

</template>

<script>

  import TablaDatos from './TablaDatos.vue'

  export default  {
    name: 'src-components-formulario',
    components: {
        TablaDatos
    },
    props: [],
    mounted () {

    },
    data () {
      return {
        formData : this.getInitialData(),
        formState : {},
        nombreMaxLength : 15,
        nombreMinLength : 5,
        edadMin : 18,
        edadMax : 120
      }
    },
    methods: {
      enviar(){
        console.log({...this.formData});

        this.formData = this.getInitialData();
        this.formState._reset();
      },

      getInitialData() {
        return {
          nombre: '',
          edad: '',
          email: ''
        }
      }

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-formulario {

  }

  input {
    margin: 7px;
  }
</style>
