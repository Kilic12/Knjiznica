<script>
import { ref } from 'vue'
import axios from 'axios'

const columns = [
  {
    name: 'id',
    label: 'ID',
    field: 'id',
    align: 'left',
    sortable: true
  },
  {
    name: 'naslov',
    label: 'Naslov',
    field: 'naslov',
    align: 'left',
    sortable: true
  },
  {
    name: 'autor',
    label: 'Autor',
    field: 'autor',
    align: 'left'
  },
  {
    name: 'opis',
    label: 'Opis',
    field: 'opis',
    align: 'left'
  },
  {
    name: 'slika',
    label: 'Slika',
    field: 'slika',
    align: 'center'
  },
  {
    name: 'stanje',
    label: 'Stanje',
    field: 'stanje',
    align: 'center'
  }
]

const books = ref([])

export default {
  setup () {
    const pagination = ref({
      rowsPerPage: 10
    })

    const loadBooks = async () => {
      try {
        const response = await axios.get('http://localhost:3000/api/knjige/')
        books.value = response.data.data
      } catch (error) {
        console.error('Error loading books:', error)
      }
    }

    return {
      columns,
      books,
      pagination,
      loadBooks
    }
  },

  mounted () {
    this.loadBooks()
  }
}
</script>

<template>
  <q-page padding>
    <div class="q-pa-md">
      <q-table
        separator="horizontal"
        title="Popis knjiga"
        title-class="text-h4 text-bold text-red-9"
        :rows="books"
        :columns="columns"
        row-key="id"
        table-class="text-black"
        table-style="border: 3px solid black;"
        table-header-style="height: 65px"
        table-header-class="bg-red-2"
        bordered
        flat
        square
      >
        <template v-slot:header="props">
          <q-tr :props="props">
            <q-th
              v-for="col in props.cols"
              :key="col.name"
              :props="props"
            >
              {{ col.label }}
            </q-th>
          </q-tr>
        </template>
        <template v-slot:body="props">
          <q-tr :props="props">
            <q-td v-for="col in props.cols" :key="col.name" :props="props">
              <span v-if="col.name !== 'slika' && col.name !== 'opis'">
                {{ col.value }}
              </span>
              <div v-if="col.name === 'opis'">
                <div class="tbl_opis">
                  {{ props.row.opis }}
                </div>
              </div>
              <q-img
                v-if="col.name === 'slika'"
                :src="props.row.slika"
                size="100px"
                class="shadow-10"
              />
            </q-td>
          </q-tr>
        </template>
      </q-table>
    </div>
  </q-page>
</template>
