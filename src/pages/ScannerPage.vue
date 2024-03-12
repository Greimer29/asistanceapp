<template>
  <q-layout view="lHh Lpr lFf">
    <QRScannerComponent
      license="DLS2eyJoYW5kc2hha2VDb2RlIjoiMjAwMDAxLTE2NDk4Mjk3OTI2MzUiLCJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSIsInNlc3Npb25QYXNzd29yZCI6IndTcGR6Vm05WDJrcEQ5YUoifQ=="
      :torchOn="torchOn" :zoomFactor="zoomFactor" :runtimeSettings="runtimeSettings" @onScanned="onScanned"
      @onPlayed="onPlayed"></QRScannerComponent>
    <q-page-sticky style="z-index:1;" position="bottom-left" :offset="[18, 18]">
      <q-fab color="blue" icon="keyboard_arrow_up" direction="up">
        <q-fab-action @click="toggleTorch" color="blue" icon="flashlight_on" />
        <q-fab-action @click="zoomIn" color="blue" icon="add" />
        <q-fab-action @click="zoomOut" color="blue" icon="remove" />
        <q-fab-action @click="goBack" color="blue" icon="arrow_back" />
      </q-fab>
    </q-page-sticky>
  </q-layout>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import QRScannerComponent from 'src/components/QRScannerComponent.vue';
import { App } from '@capacitor/app';

export default defineComponent({
  name: 'ScannerPage',
  components: { QRScannerComponent },
  setup() {
    const scanned = ref(false);
    const zoomFactor = ref(1.0);
    const torchOn = ref(false);
    const runtimeSettings = ref('');
    const router = useRouter();

    const onScanned = (result) => {
      if (result.results.length > 0 && scanned.value == false) {
        scanned.value = true;
        update(result.results);
        router.go(-1);
      }
    };

    const onPlayed = (resolution) => {
      console.log(resolution);
    }

    const toggleTorch = () => {
      torchOn.value = !torchOn.value;
    };

    const zoomIn = () => {
      zoomFactor.value = zoomFactor.value + 0.3;
    };

    const zoomOut = () => {
      zoomFactor.value = Math.max(zoomFactor.value - 0.3, 1.0);
    };

    const goBack = () => {
      router.go(-1);
    }


    onMounted(() => {
      zoomFactor.value = 1.0;
      App.addListener("backButton", () => {
        router.go(-1);
      });
    });

    return {
      onPlayed,
      torchOn,
      onScanned,
      goBack,
      zoomFactor,
      runtimeSettings,
      toggleTorch,
      zoomIn,
      zoomOut
    };
  }
});
</script>
