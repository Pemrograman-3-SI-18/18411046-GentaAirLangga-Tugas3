<template>
  <q-page>
    <div class="q-pa-md">
      <q-table
        title="Treats"
        :data="data"
        :columns="columns"
        row-key="id"
        :filter="filter"
        :loading="loading"
      >

        <template v-slot:top>
          <span class="text-h5 text-weight-light q-pa-md">
        <span class="text-blue-grey-14">Data Transaksi</span>
      </span>
          <q-space />
          <q-input borderless dense debounce="300" color="primary" v-model="filter">
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </template>

      </q-table>
    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      filter: '',
      rowCount: 10,
      columns: [
        {
          name: 'desc',
          required: true,
          label: 'Kode Transaksi',
          align: 'left',
          field: row => row.kodetransaksi,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'namapembeli', align: 'center', label: 'Nama Pembeli', field: 'namapembeli', sortable: true },
        { name: 'judulbuku', align: 'center', label: 'Judul Buku', field: 'judulbuku', sortable: true },
        { name: 'hargabuku', label: 'Harga Buku', align: 'center', field: 'hargabuku' },
        { name: 'jumlahbeli', label: 'Jumlah Beli', align: 'center', field: 'jumlahbeli' },
        { name: 'total', label: 'Total', align: 'center', field: 'total' }
      ],
      data: [
        {
          id: 1,
          kodetransaksi: 'B0001',
          namapembeli: 'Gilang Air Langga',
          judulbuku: 'Pemrograman 3',
          hargabuku: '250000',
          jumlahbeli: 2,
          total: '500000'
        },
        {
          id: 2,
          kodetransaksi: 'B0002',
          namapembeli: 'Mutiara',
          judulbuku: 'Prak Pemrograman 3',
          hargabuku: '350000',
          jumlahbeli: 3,
          total: '1050000'
        },
        {
          id: 3,
          kodetransaksi: 'B0003',
          namapembeli: 'Siti Nur Syahira Atika',
          judulbuku: 'Jeritan Akhir Zaman',
          hargabuku: '150000',
          jumlahbeli: 3,
          total: '450000'
        }
      ]

    }
  },

  methods: {
    // emulate fetching data from server
    addRow () {
      this.loading = true
      setTimeout(() => {
        const
          index = Math.floor(Math.random() * (this.data.length + 1)),
          row = this.original[Math.floor(Math.random() * this.original.length)]
        if (this.data.length === 0) {
          this.rowCount = 0
        }
        row.id = ++this.rowCount
        const addRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
        this.data = [...this.data.slice(0, index), addRow, ...this.data.slice(index)]
        this.loading = false
      }, 500)
    },

    removeRow () {
      this.loading = true
      setTimeout(() => {
        const index = Math.floor(Math.random() * this.data.length)
        this.data = [...this.data.slice(0, index), ...this.data.slice(index + 1)]
        this.loading = false
      }, 500)
    }
  }
}
</script>

<style scoped>

</style>
