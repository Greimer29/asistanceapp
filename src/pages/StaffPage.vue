<template>
  <div class="q-pa-md">
    <q-table grid flat bordered title="Personal registrado" :filter="filter" :no-data-label="!error ? '' : `${error}`">
      <template v-slot:top-right>
        <q-input borderless debounce="300" v-model="filter" placeholder="Search">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>
    </q-table>
  </div>
</template>

<script>
import { defineComponent, onMounted, ref } from 'vue'
import { useQuasar } from 'quasar'
import { api } from 'src/boot/axios'

export default defineComponent({
  name: 'StaffPage',
  setup() {
    const $q = useQuasar()
    const filter = ref('')
    const error = ref('')

    const staff = ref([])

    onMounted(() => {
      api.get('apiv1/users')
        .then(res => {
          console.log(res.data)
        })
        .catch(err => {
          console.log(err)
          error.value = err.code
        })
    })

    return {
      filter,
      error
    }
  }
})
</script>
