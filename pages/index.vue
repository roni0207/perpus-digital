<template>
  <div class="wrapper">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12">
          <h2 class="text-center text-white my-4">ISI BUKU PENGUNJUNG</h2>
            
          <div class="col-6">
            <form @submit.prevent="KirimData">
              <div class="mb-3">
                <input v-model="form.nama" type="text" class="form-control form-control-lg rounded-5" placeholder="NAMA...">
              </div>
              <div class="mb-3">
                <select v-model="form.keanggotaan" class="form-control form-control-lg from-select rounded-5">
                  <option value="">KEANGGOTAAN</option>
                  <option v-for="(member,i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
                  
                </select>
              </div>
              <div class="mb-3">
                <div class="row">
                  <div class="col-md-4">
                    <select v-model="form.tingkat" class="form-control form-control-lg form-select rounded-5 mb-2">
                      <option value="">TINGKATAN</option>
                      <option value="X">X</option>
                      <option value="XI">XI</option>
                      <option value="XII">XII</option>
                    </select>
                  </div>
                  <div class="col-md-4">
                  <select v-model="form.jurusan" class="form-control form-control-lg from-select rounded-5 mb-2">
                    <option value="">JURUSAN</option>
                    <option value="PPLG">PPLG</option>
                    <option value="TJKT">TJKT</option>
                    <option value="TSM">TSM</option>
                    <option value="DKV">DKV</option>
                    <option value="TOI">TOI</option>
                  </select>
                </div>
                <div class="col-md-4">
                  <select v-model="form.kelas" class="form-control form-control-lg from-select rounded-5 mb-2">
                    <option value="">KELAS</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                  </select>
                </div>
                  <div class="col-md-4">
                  </div>
                </div>
              </div>
              <div class="mb-3">
                <select v-model="form.keperluan"class="form-control form-control-lg from-select rounded-5">
              <option value="">KEPERLUAN</option>
              <option v-for="(item,i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
            </select>
              </div>
              <!-- <NuxtLink to="pengunjung/riwayat">
                <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">KIRIM</button>
              </NuxtLink> -->
              <input type="submit" value="kirim" class="btn btn-dark btn-lg rounded-5 px-5">
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const members = ref([])
const objectives = ref([])

const form = ref({
  nama: "",
  keanggotaan:"",
  tingkat:"",
  kelas:"",
  jurusan:"",
  keperluan:"",
})

const KirimData = async () =>{
  const { error } = await supabase.from('pengunjung').insert([form.value])
  if(error) throw error
  else navigateTo('../pengunjung/riwayat')
}

const getKeanggotaan = async () =>{
  const { data,error } = await supabase.from('keanggotaan').select('*')
  if(data) members.value = data
}

const getKeperluan = async () =>{
  const { data,error } = await supabase.from('keperluan').select('*')
  if(data) objectives.value = data
}

onMounted(() =>{
  getKeanggotaan()
  getKeperluan()
})
</script>

<style scoped>

.wrapper{  
  background-image: url('@/assets/img/4.jpg');
  background-size: cover;
  height: 100vh;
  width: 100%;
}
</style scoped>