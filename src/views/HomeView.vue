<script setup>
import Card from '@/components/Card.vue'
import axios from 'axios'
import { onMounted, ref } from 'vue'

const offersList = ref({})

onMounted(async () => {
  try {
    const { data } = await axios.get(
      `https://site--strapileboncoin--2m8zk47gvydr.code.run/api/offers?populate[0]=pictures&populate[1]=owner.avatar`,
    )
    offersList.value = data
  } catch (error) {
    console.log(error)
  }
})
</script>

<template>
  <main>
    <div class="container">
      <p v-if="!offersList.data">Chargement en cours...</p>
      <div v-else>
        <p class="topText">
          Des millions de petites annonces et autant d'occasions de se faire plaisir
        </p>
        <div class="banner">
          <img src="..\assets\img\onde-corail.svg" />
          <div>
            <p>C'est le moment de vendre</p>
            <button>
              <font-awesome-icon :icon="['far', 'plus-square']" />
              <span>Déposer une annonce</span>
            </button>
          </div>
          <img src="..\assets\img\onde-bleue.svg" />
        </div>
        <div class="offers">
          <Card
            v-for="offer in offersList.data"
            :key="offer.id"
            :offerInfos="offer.attributes"
            :id="offer.id"
          />
        </div>
      </div>
    </div>
  </main>
</template>
<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: calc(100vh - var(--header-height) - var(--footer-height));
  padding-bottom: 40px;
}
.topText {
  text-align: center;
  font-size: 24px;
  font-weight: 600;
  margin: 30px 0;
}

.banner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: var(--orange-pale);
  border-radius: 20px;
  margin-bottom: 35px;
}

.banner div {
  display: flex;
  align-items: center;
  gap: 20px;

  font-weight: bold;
}
.banner p {
  font-size: 20px;
}
img:first-child {
  border-radius: 15px 0 0 15px;
}
img:last-child {
  border-radius: 0 15px 15px 0;
}

.banner button {
  background-color: var(--orange);
  color: white;
  padding: 10px;
  border: none;
  border-radius: 10px;

  font-weight: bold;
}

.banner span {
  margin-left: 10px;
}

.offers {
  display: flex;
  flex-wrap: wrap;
  gap: 40px 15px;
}
</style>
