<template>
  <q-page class="row justify-evenly">
    <div class="full">

      <q-page-sticky position="bottom-right" :offset="[18, 18]">
        <q-btn @click="goScan" fab icon="camera_alt" color="blue" />
      </q-page-sticky>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { Clipboard } from '@capacitor/clipboard'
import { useRouter } from 'vue-router';


export default defineComponent({
  name: 'IndexPage',
  setup() {
    const router = useRouter()

    const goScan = () => {
      router.push('/scanner');
    }

    const copy = async (text) => {
      await Clipboard.write({
        string: text
      });
      Notify.create({
        message: 'Copied.'
      });
    }

    return {
      goScan,
      copy,

    }
  }
})
</script>
