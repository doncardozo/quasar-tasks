<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title class="absolute-center">
          Todo App
        </q-toolbar-title>        
      </q-toolbar>
    </q-header>

    <q-footer>
      <q-tabs>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-tabs>
    </q-footer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink'

export default {
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  data () {
    return {
      leftDrawerOpen: false,
      essentialLinks: [
        {
          title: 'ToDo',
          caption: 'ToDo',
          icon: 'list',
          link: '/'
        },
        {
          title: 'Settings',
          caption: 'Settings',
          icon: 'settings',
          link: '/settings'
        }
      ]
    }
  }
}
</script>
