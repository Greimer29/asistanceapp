<template>
  <q-toolbar class="flex-flex-center">
    <q-toolbar-title class="text-center text-italic">
      Complete el formulario para el registro
    </q-toolbar-title>
  </q-toolbar>
  <div class="flex flex-center q-pa-md">
    <q-form class="q-gutter-md text-center full-width" action="POST" method="POST">
      <q-file type="file" filled v-model="selectedFile" label="Seleccionar imagen para el susodicho">
        <template v-slot:prepend>
          <q-icon name="attachment" />
        </template>
      </q-file>
      <q-input filled label="Nombre" v-model="newUser.nombre" />
      <q-input filled label="Apellido" v-model="newUser.apellido" />
      <q-input filled label="Cargo" v-model="newUser.cargo" />
      <q-btn label="Guardar" color="positive" @click="enviar" />
    </q-form>
  </div>
</template>

<script>
import { api } from 'src/boot/axios';
import { defineComponent, ref } from 'vue';
import { useQuasar } from 'quasar';

export default defineComponent({
  name: 'RegisterForm',
  setup() {
    const $q = useQuasar()
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


    const enviar = () => {
      api.post('apiv1/users/add', {
        name: newUser.value.nombre,
        lastName: newUser.value.apellido,
        charges: newUser.value.cargo
      })
        .then(res => {
          console.log(res.data)
          $q.notify({
            position: 'top',
            color: 'positive',
            message: 'Personal registrado exitosamente'
          })
        })
        .catch(err => {
          console.log(err)
          $q.notify({
            position: 'bottom',
            color: 'negative',
            message: 'Ha ocurrido un error'
          })
        })
    }

    return {
      newUser, selectedFile, enviar
    }
  }
})
</script>
