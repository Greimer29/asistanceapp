<template>
  <q-table title="Reporte de asistencias" :columns="colums"></q-table>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'ReportComponent',
  setup() {
    const colums = ref([
      { name: 'name', field: 'nombre', label: 'Nombre' }
    ])
    return {
      colums
    }
  }
})
</script>
