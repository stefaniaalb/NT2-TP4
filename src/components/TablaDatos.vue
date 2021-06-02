<template>

  <section class="src-components-tabla-datos justify-context-center">
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">Nombre</th>
          <th scope="col">Edad</th>
          <th scope="col">Email</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ nameToShow }}</td>
          <td>{{ ageToShow }}</td>
          <td>{{ emailToShow }}</td>
        </tr>
        
      </tbody>
    </table>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-tabla-datos',
    props: [
      'nameToShow',
      'ageToShow',
      'emailToShow'
    ],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-tabla-datos {

  }
</style>
