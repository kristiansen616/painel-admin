<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar q-my-md>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-space />
         <q-icon name="far fa-moon" />
      <q-toggle
        v-model="value"
      color="yellow"
      @input="dark()"
    />
    <q-icon name="fas fa-sun" />
       <q-btn flat style="color: #ffffff" label="Alertas" @click="alert = true" />
   <q-dialog v-model="alert">
      <q-card>
        <q-card-section>
          <div class="text-h6">Alert</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Rerum repellendus sit voluptate voluptas eveniet porro. Rerum blanditiis perferendis totam, ea at omnis vel numquam exercitationem aut, natus minima, porro labore.
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
       <q-btn flat style="color: #ffffff" label="Usuário" />
       <q-btn flat style="color: #ffffff" label="Sair" />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          Menu
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'

const linksData = [
  {
    title: 'Clientes',
    caption: '',
    icon: 'home',
    link: '/'
  }
]

export default {
  name: 'MainLayout',
  components: { EssentialLink },
  data () {
    return {
      alert: false,
      confirm: false,
      prompt: false,
      value: true,

      address: '',
      leftDrawerOpen: false,
      essentialLinks: linksData
    }
  },
  methods: {
    dark (val) {
      this.$q.dark.toggle(val)
    }
  }
}
</script>
