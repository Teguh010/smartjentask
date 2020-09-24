<template>
  <q-layout view="hHh lpR fFf">

    <q-page-container class="container">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',

  data () {
    return {
    }
  }
}
</script>

<style >
.container {
height: 100vh;

}

</style>
