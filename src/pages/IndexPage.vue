<template>
  <q-card>
    <q-tabs v-model="tab" align="justify" active-color="primary" indicator-color="primary">
      <q-tab name="staff" label="Personal registrado" />
      <q-tab name="report" label="Reportes" />
    </q-tabs>
    <q-tab-panels v-model="tab">
      <q-tab-panel name="staff" label="personal">
        <div class="text-center q-mb-md">
          <q-btn color="positive" label="Pasar Asistencia" @click="askUser()" />
        </div>
        <StaffComponent />
      </q-tab-panel>
      <q-tab-panel name="report" label="Reportes">
        <ReportComponent />
      </q-tab-panel>
    </q-tab-panels>
  </q-card>
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
    const prepare = () => {
      BarcodeScanner.prepare();
    };

    const startScan = async () => {
      try {
        BarcodeScanner.hideBackground();
        const result = await BarcodeScanner.startScan();
        if (result.hasContent) {
          console.log(result.content);
        }
      } catch (error) {
        alert('Error' + error)
      }
    };

    const stopScan = () => {
      BarcodeScanner.showBackground();
      BarcodeScanner.stopScan();
    };

    const askUser = () => {
      prepare();

      const c = confirm('Do you want to scan a barcode?');

      if (c) {
        startScan();
      } else {
        stopScan();
      }
    };

    return {
      askUser,
      tab: ref('staff')
    }
  }
})
</script>
