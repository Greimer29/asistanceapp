<template>
  <q-page>
    <q-tabs v-model="tab" dense class="text-grey" active-color="primary" indicator-color="primary" align="justify"
      narrow-indicator>
      <q-tab name="staff" label="Personal" />
      <q-tab name="report" label="Reportes" />
    </q-tabs>
    <q-tab-panels v-model="tab">
      <q-tab-panel name="staff" label="personal">
        <div class="text-center q-mb-md">
          <q-btn color="positive" label="Pasar Asistencia" />
        </div>
        <StaffComponent />
      </q-tab-panel>
      <q-tab-panel name="report" label="Reportes">
        <ReportComponent />
      </q-tab-panel>
    </q-tab-panels>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'
import StaffComponent from 'src/components/StaffComponent.vue';
import ReportComponent from 'src/components/ReportComponent.vue';

export default defineComponent({
  name: 'IndexPage',
  components: {
    StaffComponent,
    ReportComponent
  },
  setup() {
    return {
      tab: ref('staff')
    }
  }
})
</script>
