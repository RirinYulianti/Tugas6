<template>
  <gambar />
  <div>
    <div class="container mt-5">
      <div class="card">
        <div class="img1">
        <img src="https://i.postimg.cc/PfQHpjys/peeking-lotso-1shz4roe0mxg93o0-removebg-preview.png" />
      </div>
        <div class="card-body">
          
          <div class="row mb-3">
            <div class="col">
              <label for="judulInput" class="form-label">Judul</label>
              <input v-model="newTitle" type="text" class="form-control" id="judulInput">
            </div>
            <div class="col">
              <label for="gambarInput" class="form-label">Gambar</label>
              <input v-model="newUrl" type="text" class="form-control" id="gambarInput">
            </div>
          </div>
          <button @click="addItem" class="btn btn-primary">Save</button>
        </div>
      </div>

      <!-- Tabel -->
      <table class="table mt-4">
        <thead>
          <tr>
            <th scope="col">Judul</th>
            <th scope="col">Gambar</th>
            <th scope="col">Aksi</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="index">
            <td>{{ item.title }}</td>
            <td><img :src="item.url" alt="Gambar" style="max-width: 100px;"></td>
            <td>
              <button class="btn btn-danger" @click="deleteItem(index)">Delete</button>
              <button class="btn btn-warning" @click="editItem(index)">Edit</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import gambar from './components/Img.vue';

const items = ref([]);
const newTitle = ref('');
const newUrl = ref('');

const fetchItems = async () => {
  try {
    const response = await axios.get('http://localhost:3000/items');
    items.value = response.data;
  } catch (error) {
    console.error('Error fetching items:', error);
  }
};

const addItem = () => {
  if (newTitle.value && newUrl.value) {
    items.value.push({ title: newTitle.value, url: newUrl.value });
    newTitle.value = '';
    newUrl.value = '';
  }
};

const deleteItem = (index) => {
  items.value.splice(index, 1);
};

const editItem = (index) => {
  // Implementasi edit item
};

onMounted(() => {
  fetchItems();
});
</script>

<style scoped>
body {
  background-color: black;
}

.btn{
  margin-right: 10px;
}

.card{
  background-color: white;
}
.form-control{
  background-color: transparent;
}
.img1 img {
    width: 10%;
    position: fixed;
    display: inline;
    top: 21%;
    left: 32%;
   }

</style>
