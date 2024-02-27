<template>
  <q-page>
    <q-tabs v-model="tab" animated>
      <q-tab name="staff" label="Personal" />
      <q-tab name="report" label="Reportes" />
    </q-tabs>
    <q-tab-panels v-model="tab">
      <q-tab-panel name="staff" label="personal">
        <div class="text-center q-mb-md">
          <q-btn color="positive" label="Pasar Asistencia" @click="startScan()" />
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
import { BarcodeScanner } from '@capacitor-community/barcode-scanner';

export default defineComponent({
  name: 'IndexPage',
  components: {
    StaffComponent,
    ReportComponent
  },
  setup() {
    const startScan = async () => {
      // Check camera permission
      // This is just a simple example, check out the better checks below
      await BarcodeScanner.checkPermission({ force: true });

      // make background of WebView transparent
      // note: if you are using ionic this might not be enough, check below
      BarcodeScanner.hideBackground();

      const result = await BarcodeScanner.startScan(); // start scanning and wait for a result

      // if the result has content
      if (result.hasContent) {
        console.log(result.content); // log the raw scanned content
      }
    }
    return {
      startScan,
      tab: ref('staff')
    }
  }
})
</script>
