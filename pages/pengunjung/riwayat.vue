<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12">
          <h2 class="text-center my-4 text-light">RIWAYAT KUNJUNGAN</h2>
          <div class="my-3">
            <input type="search" class="form-control form-control-lg rounded-5" placeholder="Filter...">
          </div>
          <div class="my-3">menampilkan 1 dari 1</div>
          <table class="table">
            <thead>
              <tr>
                <td>NO</td>
                <td>NAMA</td>
                <td>KEANGGOTAAN</td>
                <td>KELAS</td>
                <td>KEPERLUAN</td>
                <td>Tanggal&Waktu</td>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(visitors,i) in visitors" :key="i" class="text-center text-white">
                <td>{{ i+1 }}.</td>
                <td>{{ visitors.nama }}</td>
                <td>{{ visitors.keanggotaan.nama }}</td>
                <td>{{ visitors.tingkat}}-{{ visitors.jurusan }}{{ visitors.kelas }}</td>
                <td>{{ visitors.keperluan.nama }}</td>
                <td>{{ visitors.tanggal }}</td>
              </tr>
            </tbody>
          </table>
          <nuxt-link to="/buku" class="btn btn-back btn-lg rounded-5 px-5">cari buku</nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])

const getPengunjung = async () =>{
  const { data,error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
  if(data) visitors.value = data
}

onMounted(() => {
  getPengunjung()
})
</script>


<style scoped>
.btn-back{
  background-color: rgb(28, 19, 154);
  color: rgb(214, 245, 10);
  border: 2px solid rgb(20, 169, 104);
}

table{
  background-color: #fff;
  border: 2px solid black;
  border-radius: 10px;
}

.table td{
  color: rgb(0, 0, 0);
  border: 2px solid black;
}

.content{
  background-image:url(~/assets/img/4.jpg);
  background-size: cover;
  height: 100vh;
}
</style>