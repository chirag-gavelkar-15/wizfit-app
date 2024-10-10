<template>
  <div class="wizfit-container">
    <header class="header">
      <img src="../assets/banner.png" alt="WizFit Challenge Banner" class="banner" />
     
    </header>
    <section>
      <div class="watch-section">
        <h1>What is WizFit Challenge ??</h1>  
        <button class="watch-button">Watch Video</button>
      </div>
      <img src="../assets/player.png" alt="logo" class="logo" />

    </section>
    <section class="main-section">
    <div class="search-section">
      <input
        v-model="searchQuery"
          @input="fetchSchools"
        placeholder="Search School Name"
        class="search-input"
      />
    </div>
   
      <h1>Are you ready to take Challenge ?</h1>
        <img src="../assets/apple-store.png" alt="apple-store" class="storelogo" />
      <img src="../assets/goolge-store.png" alt="goolge-store" class="storelogo" />

    <div class="schools-list" v-if="schools.length">
      <div class="school-item" v-for="school in schools" :key="school.id">
          <p>{{ school.school_name }}</p>
        <button class="join-button">Join Campaign</button>
      </div>
    </div>

    <div v-else class="no-results">
        <p>No data found</p>
    </div>
       </section>
  </div>
 </template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    const schools = ref([]);
      const searchQuery = ref("");

    const fetchSchools = async () => {
      try {
        const response = await fetch(
          `http://api.devharlemwizardsinabox.com/campaign/campaign_school_list/?search=${searchQuery.value}`
        );
        const data = await response.json();


         console.log(data.school_list,'data')
        schools.value = data.school_list || [];
      } catch (error) {
          console.error("Error fetching schools:", error);
        schools.value = [];
      }
    };

    onMounted(() => {
      fetchSchools();
    });

    return {
      schools,
      searchQuery,
      fetchSchools,
    };
  },
};
</script>

<style scoped>
.wizfit-container {
  font-family: 'Arial', sans-serif;
  text-align: center;
  color: black;
 
}

.header {
  
  color: white;

}

.banner {
  width: 100%;
  
}


.watch-section {
  background-color: #f4f4f4;
   border-radius: 10px;
  padding: 30px 20px;
    text-align: center;
  max-width: 600px;
   margin: 20px auto;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.watch-section h1 {
  font-size: 2rem;
  color: #004E95;
  margin-bottom: 20px;
}

.watch-button {
  background-color: #004E95;
  color: #fff;
  border: none;
    border-radius: 5px;
  padding: 12px 30px;
   font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.watch-button:hover {
  background-color: #003B73;
}

.logo {
  width: 250px;
  
}


.main-section {
  background-color: #fff;
 border-radius: 8px;
  box-shadow: 1px 4px 8px rgba(0, 0, 0, 0.1);
    padding: 20px;
  max-width: 600px;
   margin: 20px auto;
  text-align: center;
}
.storelogo {
  width: 150px;
 
}

.search-section {
  margin: 20px auto;
    width: 100%;
  max-width: 400px;
}

.search-input {
  width: 100%;
  padding: 10px;
    font-size: 16px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

.schools-list {
  display: flex;
   flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.school-item {
width: 100%;
  max-width: 400px;
    padding: 10px;
   background-color: #f5f5f5;
  border-radius: 8px;
  margin-bottom: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.join-button {
  background-color: #e91e63;
  color: white;
  padding: 10px 20px;
   border: none;
  border-radius: 4px;
  cursor: pointer;
}

.join-button:hover {
   background-color: #d81b60;
}


.no-results {
   margin-top: 20px;
  color: #d32f2f;
}


@media (max-width: 768px) {
  .watch-section h1 {
    font-size: 1.6rem;
  }

  .watch-button {
    padding: 10px 25px;
     font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .watch-section h1 {
    font-size: 1.4rem;
  }

  .watch-button {
    padding: 8px 20px;
    font-size: 0.85rem;
  }
}

</style>
