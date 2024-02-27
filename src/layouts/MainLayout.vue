<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>

        <q-toolbar-title>
          <q-btn flat label="Quasar App" to="/" />
        </q-toolbar-title>

        <div>
          <q-btn label="Agregar personal" outline color="orange" to="/person" />
        </div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  setup() {

    return {
    }
  }
})
</script>
