<template>
  <div class="flex flex-center q-pa-md">
    <q-form class="q-gutter-md text-center full-width">
      <q-file type="file" filled v-model="selectedFile" label="Seleccionar imagen para el susodicho">
        <template v-slot:prepend>
          <q-icon name="attachment" />
        </template>
      </q-file>
      <q-input filled label="Nombre" v-model="newUser.nombre" />
      <q-input filled label="Apellido" v-model="newUser.apellido" />
      <q-input filled label="Cargo" v-model="newUser.cargo" />
      <q-btn label="Guardar" color="positive" />
    </q-form>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'RegisterForm',
  setup() {
    const selectedFile = ref()
    const newUser = ref({
      nombre: '',
      apellido: '',
      cargo: ''
    })

    if (selectedFile.value != null) {
      const formData = new FormData();
      formData.append("image", selectedFile.value);
    }

    return {
      newUser, selectedFile
    }
  }
})
</script>
