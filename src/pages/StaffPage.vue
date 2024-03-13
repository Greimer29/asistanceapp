<template>
  <div class="q-pa-md">
    <q-card class="no-shadow">
      <q-card-section>
        <div class="text-h6 text-grey-8 text-center">
          Personal del departamento
        </div>
      </q-card-section>
      <q-separator />
      <q-card-section>
        <q-table grid flat hide-bottom :rows-per-page-options="[0]" bordered title="Personal registrado"
          :filter="filter" :no-data-label="!error ? '' : `${error}`" :rows="rows" :columns="columns">
          <template v-slot:top-right>
            <q-input borderless debounce="300" v-model="filter" placeholder="Search">
              <template v-slot:append>
                <q-icon name="search" />
              </template>
            </q-input>
          </template>
          <template v-slot:item="props">
            <StaffCards :nombre="props.row.nombre" :apellido="props.row.apellido" :cargo="props.row.cargo"></StaffCards>
          </template>
        </q-table>
      </q-card-section>
    </q-card>
  </div>
</template>

<script>
import { defineComponent, onMounted, ref } from 'vue'
import StaffCards from 'src/components/StaffCards.vue'
import { useQuasar } from 'quasar'
import { api } from 'src/boot/axios'

export default defineComponent({
  name: 'StaffPage',
  components: {
    StaffCards
  },
  setup() {
    const $q = useQuasar()
    const filter = ref('')
    const error = ref('')
    const staff = ref([])

    const columns = [
      { name: 'nombre', label: 'Nombre', field: 'nombre' },
      { name: 'apellido', label: 'Apellido', field: 'apellido' },
      { name: 'cargo', label: 'Cargo', field: 'cargo' },
    ]

    onMounted(() => {
      api.get('apiv1/users')
        .then(res => {
          console.log(res.data)
          staff.value = res.data
        })
        .catch(err => {
          console.log(err)
          error.value = err.code
        })
    })

    return {
      filter,
      error,
      rows: staff,
      columns
    }
  }
})
</script>
