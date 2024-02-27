<template>
 <q-banner inline-actions rounded class="bg-black text-white">
  <div class="flex q-gutter-md">
  <q-avatar >
      <img font-size="52px" src="https://cdn.quasar.dev/img/avatar.png" >
  </q-avatar>
    <div class="text-bold">
      {{ staff.name }}
      {{ staff.name }}
      <div>{{ staff.name }}</div>
    </div>
  </div>
    <template v-slot:action>
      <q-btn flat color="negative" label="Salida" />
    </template>
  </q-banner>
</template>

<script>
import {defineComponent,ref} from 'vue'
export default defineComponent({
  setup(){
    const staff = ref({
      name:'Greimer',
      position:'Director de servicios estudiantiles'
    })
    return{
      staff
    }
  }
})
</script>
