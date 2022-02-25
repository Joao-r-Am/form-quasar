<template>
  <q-page class="container" padding>
    <p class="text-h4">Formulario</p>
    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="row q-col-gutter-md"
      ref="myForm"
    >
      <q-input
        outlined
        v-model="form.nome"
        color="blue"
        label="Nome"
        class="col-md-12 col-sm-12 col-xs-12"
        :rules="[(val) => (val && val.length > 0) || 'Nome obrigatorio']"
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
        label="idade"
        :rules="[
          (val) => (val !== null && val !== '') || 'idade Obrigatoria!',
          (val) => (val > 0 && val < 120) || 'idade inválida',
        ]"
      >
        <template v-slot:prepend>
          <q-icon name="person" />
        </template>
      </q-input>

      <q-input
        v-model="form.email"
        label="Email"
        suffix="@gmail.com"
        outlined
        class="col-md-12 col-sm-12 col-xs-12"
        :rules="[(val) => (val && val.length > 0) || 'Nome obrigatorio']"
      >
        <template v-slot:prepend>
          <q-icon name="mails" />
        </template>
      </q-input>

      <q-input
        v-model="form.telefone"
        label="Telefone"
        outlined
        class="col-md-12 col-sm-12 col-xs-12"
        mask="(##) #####-####"
        unmasked-value
        :rules="[
          (val) => (val && val.length > 0) || 'Numero de telefone obrigatorio',
          (val) => val.length === 11 || 'Numero de telefone inválido',
        ]"
      />

      <q-select
        outlined
        v-model="form.tipoPessoa"
        :options="optionsTiposPessoa"
        label="Tipo de pessoa"
        class="col-md-12 col-sm-12 col-xs-12"
        emit-value
        map-options
        :rules="[
          (val) => (val && val.length > 0) || 'Tipo de pessoa obrigatorio',
        ]"
      />
      <span class="text-bold">Selecione seu genero</span>
      <q-option-group
        :options="optionsGenero"
        label="Genero"
        type="radio"
        v-model="form.genero"
        class="col-md-12 col-sm-12 col-xs-12"
      />
      <span class="text-bold">Quer receber notificações?</span>
      <q-option-group
        label="deseja receber notificações"
        :options="optionsNotificar"
        type="checkbox"
        v-model="form.notificar"
        class="col-md-12 col-sm-12 col-xs-12"
      />

      <div class="col-12">
        <q-btn
          label="Cadastrar"
          type="submit"
          color="primary"
          class="float-right"
        />
        <q-btn
          label="Reset"
          type="submit"
          color="defaul"
          class="float-right text-grey-10 q-mr-md"
        />

        <q-toggle
          v-model="form.receberEmail"
          color="pink"
          icon="mail"
          label="Deseja receber e-mails?"
        />
      </div>
    </q-form>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      form: {
        nome: "",
        idade: null,
        email: "",
        telefone: "",
        tipoPessoa: "",
        genero: "NA",
        notificar: [],
        receberEmail: false
      },
      optionsTiposPessoa: [
        { label: "Pessoa Física", value: "pf" },
        { label: "Pessoa Juridica", value: "pj" },
      ],
      optionsGenero: [
        { label: "Não informar", value: "NA", color: "red" },
        { label: "Masculino", value: "M", color: "blue" },
        { label: "Feminino", value: "F", color: "green" },
      ],
      optionsNotificar: [
        { label: "Receber Notificações:", value: "notiTrue" },
        { label: "Receber Promoções", value: "promoTrue", color: "green" },
        { label: "Receber Novidade", value: "NovTrue", color: "red" },
      ],
    };
  },
  methods: {
    onSubmit() {
      console.log(this.form.nome);
      console.log(this.form.idade);
      console.log(this.form.email);
      console.log(this.form.telefone);
      console.log(this.form.tipoPessoa);
      console.log(this.form.genero);
      console.log(this.form.notificar);
      console.log(this.form.receberEmail)

      this.$q.notify({
        message: "Cadastrado com sucesso",
        color: "positive",
        icon: "check_circle_outline",
      });
      this.onReset();
    },
    async onReset() {
      await this.resetForm();
      this.$refs.myForm.resetValidation();
    },
    async resetForm() {
      this.form = {
        nome: "",
        idade: null,
        email: "",
        telefone: "",
        tipoPessoa: "",
        genero: "",
        notificar: [],
        receberEmail: false
      };
    },
  },
};
</script>
