<script setup>
import { ref } from 'vue';
import DataTable from 'datatables.net-vue3';
import DataTablesCore from 'datatables.net-bs5';

DataTable.use(DataTablesCore);

const columns = [
  { data: 'No' },
  { data: 'Tanggal' },
  { data: 'Nama_Acara' },
  { data: 'Keterangan' },
  { data: 'Status',
    render : function(data, type, row) {
      let status = '<span class="badge bg-success">'+data+'</span>' 
      if (data != "Selesai") {
        status = '<span class="badge bg-danger">'+data+'</span>' 
        
      }
      return status
    }    
  },
  {"defaultContent":`
    <button type='button' data-bs-toggle='modal' data-bs-target='#exampleModal' class='btn btn-danger'> Batalkan </button>
    <button type='button' data-bs-toggle='modal' data-bs-target='#exampleModal' class='btn btn-primary'> Selesai </button>
    `}
];

let showModal = ref(false);

</script>

<template> 
  <div class="container">
    <div class="d-flex justify-content-between m-5">
      <h2>Data Acara</h2>
      <button @click="showModal = true" class="btn btn-success">Tambah Acara</button>
    </div>
    <div class="row">
      <div class="col-3">
        <select class="form-select mb-3">
          <option selected>-- Pilih Status --</option>
          <option value="1">Selesai</option>
          <option value="2">Belum selesai</option>
        </select>
      </div>
    </div>
    <DataTable
      :columns="columns"
      ajax="/data.json"
      class="table table-hover table-striped"
      width="100%"
    >
      <thead>
        <tr>
          <th>No</th>
          <th>Tanggal</th>
          <th>Nama Acara</th>
          <th>Keterangan</th>
          <th>Status</th>
          <th>Action</th>
        </tr>
      </thead>
    </DataTable>
  </div>

  <div v-if="showModal" class="modal">
      <div class="modal-content">
        <!-- Modal content -->
        <div class="modal-header">
          <h5 class="modal-title">Tambah Acara</h5>
          <button type="button" @click="showModal = false" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <form>
            <div class="mb-3">
              <label for="tanggal">Tanggal</label>
              <input type="date" class="form-control" id="tanggal" placeholder="date">
            </div>
            <div class="mb-3">
              <label for="nama_acara">Nama Acara</label>
              <input type="text" class="form-control" id="nama_acara" placeholder="Nama Acara">
            </div>
            <div class="mb-3">
              <label for="keterangan">Keterangan</label>
              <textarea class="form-control" id="keterangan" rows="3"></textarea>
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" @click="showModal = false" data-bs-dismiss="modal">Close</button>
          <button type="button" class="btn btn-primary">Save changes</button>
        </div>
      </div>
    </div>
</template>

<style>
@import 'bootstrap';
@import 'datatables.net-bs5';

/* Modal styles */
  .modal {
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    z-index: 9999;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
  }

.modal-content {
  background-color: #fff;
  border-radius: 5px;
  padding: 20px;
  max-width: 500px;
  width: 90%;
  max-height: 80%;
  overflow-y: auto;
}

.modal-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
</style>