<script setup>
import { ref } from 'vue'
import TheModal from './components/TheModal.vue' 
import { onMounted } from 'vue';
import PeopleTable from './components/PeopleTable.vue';

const showModalHello = ref(false)
const showModalBye = ref(false)

const peoples = ref([]);


const fetchData = async () => {
  try {
    const response = await fetch('http://localhost:3000/peoples');
    if (!response.ok) {
      throw new Error('Erreur lors de la récupération des données');
    }
    const data = await response.json();
    peoples.value = data;
  } catch (error) {
    console.error(error.message);
  }
}


onMounted(() => {
  fetchData();
});

const columns = [
  { name: 'name', label: 'Nom' },
  { name: 'company', label: 'Entreprise' },
  { name: 'isActive', label: 'Actif' }
];

</script>

<template>
  <button class="btn btn-primary" @click="showModalHello = true">Dites bonjour 👋</button>
  <button class="btn btn-primary ml-2" @click="showModalBye = true">Au revoir 👋</button>

  <TheModal :showModal="showModalHello" @close="showModalHello = false">
    <p class="py-4">
      Lorem ipsum, dolor sit amet consectetur adipisicing elit. Laudantium, rem nihil. Ullam
      placeat natus aliquam, molestias cumque, ipsam praesentium sint culpa animi voluptatibus
      itaque libero debitis aliquid laudantium nam quam!
    </p>
  </TheModal>

  <TheModal :showModal="showModalBye" @close="showModalBye = false">
    <img src="./assets/bye.gif" alt="Cat say bye" />
  </TheModal>

<PeopleTable :items="peoples" :columns="columns">
  <template #actions="{ id }">
    <div class="flex items-center space-x-2">
      <button class="btn btn-primary btn-sm" @click="openDetailsModal(id)">Détails</button>
      <button class="btn btn-secondary btn-sm" @click="openMessageModal(id)">Message</button>
    </div>
  </template>
</PeopleTable>

  
</template>


