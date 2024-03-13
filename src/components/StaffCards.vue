<template v-slot:item>
  <div class="q-pa-xs col-xs-12 col-sm-6 col-md-4 col-lg-3">
    <q-card class="no-shadow" bordered>
      <q-card-section class="text-center">
        <q-avatar size="100px" class="shadow-10">
          <img :src="avatar">
        </q-avatar>
      </q-card-section>

      <q-card-section class="q-pt-none text-center ">
        <div class="text-h6  text-grey-8">
          {{ nombre }} {{ apellido }}
        </div>
        <div class="text-center">
          <div class="text-bold"> {{ cargo }}</div>
        </div>
      </q-card-section>
      <q-card-actions v-show="true" class="flex-center">
        <q-btn flat round icon="mail" class="bg-indigo-7 text-white" />
        <q-btn flat round icon="facebook" class="bg-info text-white" />
        <q-btn flat round icon="telegram" class="bg-indigo-8 text-white" />
      </q-card-actions>
    </q-card>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'StaffCards',
  props: ['nombre', 'apellido', 'cargo', 'avatar'],
  setup() {

  }
})
</script>
