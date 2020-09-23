<template>
<q-page class="q-pa-md">
    <q-form
      @submit="onSubmit"
      class="q-gutter-md"
      v-model="sub"
    >
    <div class="text-h4 doc-h6">Cliente - Busca</div>
    <hr>
    <div class="row q-gutter-x-md justify-center">
        <div class="col-xs-10 col-sm-6 col-md-5">
      <q-input
        filled
        v-model="usuario.name"
        label="Seu nome*"
        hint="Nome e Sobrenome"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'por favor, escreva algo']"
      />
      </div>

         <div class="col-xs-10 col-sm-6 col-md-5">
      <q-select filled v-model="usuario.muni" :options="['Areal', 'Rio das Ostras', 'Volta Redonda']" hint="" label="Município" />
    </div>
    </div>
    <div class="row q-gutter-x-md justify-center">
    <div class="col-xs-10 col-sm-6 col-md-5">
       <q-input
        filled
        v-model="usuario.Doc"
        type="number"
        label="Seu Documento*"
        hint="RJ,CNPJ,CPF"
        lazy-rules
        :key="data.doc"
        :rules="[ val => val && val.length <= 12  || 'Número invalido']"
      />
      </div>
        <div class="col-xs-10 col-sm-6 col-md-5">
      <q-input
        filled
        v-model="usuario.email"
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
       <q-select filled v-model="usuario.situacao" :options="['Ativo', 'Inativo']" hint="" label="Situação" />
    </div>
    <div class="col-xs-10 col-sm-6 col-md-5">
       <q-input
        filled
        v-model="usuario.bairro"
        type="text"
        label="Seu Bairro*"
        hint=""
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Nome invalido']"
      />
      </div>
</div>

      <div class="row justify-center">
        <q-btn size="15px" class="q-px-xl q-py-xs" label="Pesquisar" @click="enviar" v-model="sub" type="submit" color="primary"/>
      </div>
    </q-form>
    <br>
    <p class="resultado text-center breadcrumb">Foram encontrados 6702 registros, divididos em 336 página(s)</p>

 <div class="q-pa-md q-gutter-sm">
 <q-card>
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
    >

<template v-slot:body-cell-name="props">
        <q-td :props="props">
        <div>
            {{ usuario.name }}
        </div>
          <div class="my-table-details">
            {{ props.row.name }}
          </div>
        </q-td>
      </template>
      <template v-slot:body-cell-email="props">
        <q-td :props="props">
        <div>
            {{ usuario.email }}
        </div>
        </q-td>
      </template>
      <template v-slot:body-cell-bairro="props">
        <q-td :props="props">
        <div>
            {{ usuario.bairro }}
        </div>
        </q-td>
      </template>
      <template v-slot:body-cell-Doc="props">
        <q-td :props="props">
        <div>
            {{ usuario.Doc }}
        </div>
        </q-td>
      </template>
      <template v-slot:body-cell-muni="props">
        <q-td :props="props">
        <div>
            {{ usuario.muni }}
        </div>
        </q-td>
      </template>
      <template v-slot:body-cell-situacao="props">
        <q-td :props="props">
        <div>
            {{ usuario.situacao }}
        </div>
        </q-td>
      </template>
     <template v-slot:body-cell-detail="props">
          <q-td :props="props">
            <q-btn @click="employee_dialog=true" dense round color="secondary" icon="pageview"/>
          </q-td>
        </template>
        <template v-slot:body-cell-action="props">
          <q-td :props="props">
            <div class="q-gutter-sm">
              <q-btn dense color="primary" icon="edit"/>
              <q-btn dense color="red" icon="delete"/>
            </div>
          </q-td>
        </template>
         </q-table>
    </q-card>
 <q-dialog v-model="employee_dialog">
      <q-card class="my-card" flat bordered>
        <q-card-section>
          <div class="text-h6">
            Employee Details
            <q-btn round flat dense icon="close" class="float-right" color="grey-8" v-close-popup></q-btn>
          </div>
        </q-card-section>
        <q-card-section horizontal>
          <q-card-section class="q-pt-xs">

          </q-card-section>
          <q-table
          v-model="separator"
          dense
          :data="data"
          :columns="columns"
          row-key="email"
          :separator="separator"
          :options="[
          // { label: 'Horizontal', value: 'horizontal' },
          // { label: 'Vertical', value: 'vertical' },
          // { label: 'Cell', value: 'cell' },
          //{ label: 'None', value: 'none' },
        ]"
    >

        <template v-slot:body-cell-email="props">
        <q-td :props="props">
        <div>
            {{ usuario.email }}
        </div>
        <br>
           <div class="q-gutter-sm">
              <q-btn dense color="primary" icon="edit"/>
              <q-btn dense color="red" icon="delete"/>
            </div>
        </q-td>
      </template>
      </q-table>
        </q-card-section>

        <q-separator/>

      </q-card>
    </q-dialog>
    </div>
 </q-page>
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
.my-table-details {
  font-size: 1.1em;
  max-width: 100px;
  white-space: normal;
  margin-top: 4px;
}
</style>
<script>
export default {
  data () {
    return {
      usuario: {
        name: '',
        muni: '',
        Doc: '',
        email: '',
        situacao: '',
        bairro: ''
      },
      alert: false,
      confirm: false,
      prompt: false,
      employee_dialog: false,
      sub: false,

      address: '',
      separator: 'cell',
      columns: [
        {
          name: 'name',
          required: true,
          label: 'Nome',
          align: 'center',
          field: row => row.name,
          format: val => `${val}`,
          sortable: true,
          style: 'height: 70px',
          classes: 'my-special-class',
          headerStyle: 'height: 50px;'
        },
        { name: 'muni', label: 'Município', field: 'fat', sortable: true, align: 'center' },
        { name: 'Doc', label: 'Documento', field: 'carbs', align: 'center' },
        { name: 'email', label: 'E-mail', field: 'protein', align: 'center' },
        { name: 'situacao', label: 'Situação', field: 'sodium', align: 'center' },
        { name: 'bairro', label: 'Bairro', field: 'calcium', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10), align: 'center' },
        { name: 'detail', label: 'Detalhes', field: 'detail', sortable: true, align: 'center' },
        { name: 'action', label: 'Ações', field: 'action', sortable: true, align: 'center' }
      ],
      data: [
        {

        }
      ]
    }
  },

  methods: {
    onSubmit () {
      this.$q.notify({
        message: 'Submetido',
        color: 'green-4',
        icon: 'cloud_done',
        textcolor: 'white'
      })
    },
    enviar () {
      this.sub = true
    }
  }
}
</script>
