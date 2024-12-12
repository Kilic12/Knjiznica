<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title class="text-h4 text-weight-bold">
          Knjižnica
        </q-toolbar-title>
        <q-space />
      </q-toolbar>
    </q-header>

    <q-drawer show-if-above>
      <q-list>
        <q-item
          v-for="item in linkedList"
          :key="item.title"
          clickable
          tag="router-link"
          :to="item.link"
        >
          <q-item-section avatar>
            <q-icon :name="item.icon" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ item.title }}</q-item-label>
            <q-item-label caption>{{ item.caption }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  setup () {
    return {
      linkedList: [
        { title: 'Naslovnica', caption: 'Početna stranica', icon: 'home', link: '/' },
        { title: 'Popis knjiga', caption: 'Pregled knjiga', icon: 'book', link: '/popisKnjiga' },
        { title: 'Pretraživanje', caption: 'Traži knjige', icon: 'search', link: '/pretrazivanje' },
        { title: 'O nama', caption: 'Informacije o knjižnici', icon: 'info', link: '/o_nama' },
        { title: 'Lokacija', caption: 'Pronađi nas', icon: 'location_on', link: '/lokacija' },
        { title: 'Login', caption: 'Prijava', icon: 'login', link: '/login' },
        { title: 'Registracija', caption: 'Novi korisnik', icon: 'person_add', link: '/registracija' }
      ]
    }
  }
}
</script>

<style scoped>
</style>
