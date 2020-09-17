<template>
  <div class="q-pa-md">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
    <div class="text-h4 doc-h6">Cliente - Busca</div>
    <hr>
    <div class="row q-gutter-x-md justify-center">
        <div class="col-xs-10 col-sm-6 col-md-5">
      <q-input
        filled
        v-model="name"
        label="Seu nome*"
        hint="Nome e Sobrenome"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'por favor, escreva algo']"
      />
      </div>

         <div class="col-xs-10 col-sm-6 col-md-5">
       <q-select
         filled
          v-model="muni"
        use-input
        input-debounce="0"
        label="Município"
        :options="['Areal', 'Rio das Ostras', ['Volta Redonda']]"
        @filter="filterFn"
        behavior="menu"
      />
    </div>
    </div>
    <div class="row q-gutter-x-md justify-center">
    <div class="col-xs-10 col-sm-6 col-md-5">
       <q-input
        filled
        v-model="Doc"
        type="number"
        label="Seu Documento*"
        hint="RJ,CNPJ,CPF"
        lazy-rules
        :rules="[ val => val && val.length <= 12  || 'Número invalido']"
      />
      </div>
        <div class="col-xs-10 col-sm-6 col-md-5">
      <q-input
        filled
        v-model="email"
        type="text"
        label="Seu E-mail*"
        hint="Não esqueça do @"
        lazy-rules
        :rules="[ val => val && val.length > 0  || 'E-mail invalido']"
      />
    </div>
</div>

<div class="row q-gutter-x-md justify-center">
      <div class="col-xs-10 col-sm-6 col-md-5">
       <q-select filled v-model="situacao" :options="['Ativo', 'Inativo']" hint="" label="Situação" />
    </div>
    <div class="col-xs-10 col-sm-6 col-md-5">
       <q-input
        filled
        v-model="bairro"
        type="text"
        label="Seu Bairro*"
        hint=""
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Nome invalido']"
      />
      </div>
</div>

      <div class="row justify-center">
        <q-btn size="15px" class="q-px-xl q-py-xs" label="Enviar" v-model="sub" type="submit" color="primary"/>
      </div>
    </q-form>
    <br>
    <p class="resultado text-center breadcrumb">Foram encontrados 6702 registros, divididos em 336 página(s)</p>

 <div class="q-pa-md q-gutter-sm">
    <q-table
     v-model="separator"
      title="Treats"
      dense
      :data="data"
      :columns="columns"
      row-key="name"
      :separator="separator"
       :options="[
       // { label: 'Horizontal', value: 'horizontal' },
       // { label: 'Vertical', value: 'vertical' },
       // { label: 'Cell', value: 'cell' },
      //{ label: 'None', value: 'none' },
      ]"
    />
</div>
  </div>
</template>
<style>
.resultado {
    font-family: Arial;
    color: #222;
    font-size: 15px;
}
.breadcrumb {
    padding: 8px 15px;
    margin-bottom: 20px;
    list-style: none;
    background-color: #f5f5f5;
    border-radius: 4px;
}
</style>
<script>
export default {
  data () {
    return {
      current: 1,
      model: null,
      name: null,
      muni: null,
      Doc: null,
      email: null,
      situacao: null,
      bairro: null,
      accept: false
    }
  },

  methods: {
    onSubmit () {
      if (this.sub === true) {
        this.$q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'warning',
          message: 'você precisa aceitar a licença e termos de primeira'
        })
      } else {
        this.$q.notify({
          color: 'green-4',
          textColor: 'white',
          icon: 'cloud_done',
          message: 'submetido'
        })
      }
    },

    onReset () {
      this.name = null
      this.muni = null
      this.Doc = null
      this.email = null
      this.situacao = null
      this.bairro = null
      this.accept = false
    }
  }
}
</script>

<script>
export default {
  data () {
    return {
      alert: false,
      confirm: false,
      prompt: false,

      address: '',

      separator: 'cell',

      columns: [
        {
          name: 'name',
          required: true,
          label: 'Nome/Razão',
          align: 'left',
          field: row => row.name,
          format: val => `${val}`,
          sortable: true,
          style: 'max-width: 400px; height: 70px',
          classes: 'my-special-class',
          headerStyle: 'height: 50px; font-size: 20px',
        },
        { name: 'Endereço', label: 'Endereço', field: 'fat', sortable: true},
        { name: 'Bairro', label: 'Bairro', field: 'carbs' },
        { name: 'Município', label: 'Município', field: 'protein'},
        { name: 'Contato', label: 'Contato', field: 'sodium' },
        { name: 'Opções', label: 'Opções', field: 'calcium', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
      ],
      data: [
        {
          name: 'RADIO IMAGEM RADIOLOGIA LTDA',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          sodium: 87,
          calcium: '14%',
          iron: '1%'
        },
        {
          name: 'Lilian Cristina Salgueiro',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          sodium: 129,
          calcium: '8%',
          iron: '1%'
        },
        {
          name: 'ASSISTÊNCIA MÉDICA IMAGEM EIRELI -ME',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          sodium: 337,
          calcium: '6%',
          iron: '7%'
        },
        {
          name: 'CAF CENTRO DE ATENDIMENTO FISIOTERÁPICO',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          sodium: 413,
          calcium: '3%',
          iron: '8%'
        },
        {
          name: 'HOSPITAL POPULAR DE MEDICINA VETERINÁRIA LTDA',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          sodium: 327,
          calcium: '7%',
          iron: '16%'
        },
        {
          name: 'SENCE & CHAMMA CLÍNICA ODONTOLOGICA LTDA-ME',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          sodium: 50,
          calcium: '0%',
          iron: '0%'
        },
        {
          name: 'A4 CLÍNICA ODONTOLÓGICA LTDA.',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          sodium: 38,
          calcium: '0%',
          iron: '2%'
        },
        {
          name: 'CENTRO ODONTOLOGICO SORRIA RIO QUEIMADOS LTDA',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          sodium: 562,
          calcium: '0%',
          iron: '45%'
        },
        {
          name: 'Mayene Bittencourt Burity',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          sodium: 326,
          calcium: '2%',
          iron: '22%'
        }
      ]
    }
  }
}
</script>
