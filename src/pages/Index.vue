<template>
  <q-page class="container" padding>
    <p class="text-h4">Formulario</p>
    <div class="row">
      <q-input
        outlined
        v-model="form.nome"
        color="blue"
        label="Nome"
        class="col-md-12 col-sm-12 col-xs-12"
      >
      <template v-slot:prepend>
          <q-icon name="person" />
        </template>
      </q-input>
      <p>{{ form.nome }}</p>

      <q-input
        v-model.number="form.idade"
        type="number"
        outlined
        class="col-md-12 col-sm-12 col-xs-12"
      />

    </div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      form: {
        nome: "",
        idade: "",
      },
    };
  },
};
</script>
