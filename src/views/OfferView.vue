<script setup>
import { onMounted, ref, computed } from 'vue'
import axios from 'axios'
const props = defineProps({
  id: String,
})

const offerInfo = ref(null)

onMounted(async () => {
  try {
    const { data } = await axios.get(
      `https://site--strapileboncoin--2m8zk47gvydr.code.run/api/offers/${props.id}?populate[0]=pictures&populate[1]=owner.avatar`,
    )
    offerInfo.value = data.data
  } catch (error) {
    console.log(error)
  }
})

const formatDate = computed(() => {
  return offerInfo.value.attributes.publishedAt?.split('T')[0].split('-').reverse().join('/')
})
</script>
<template>
  <div class="container">
    <p v-if="offerInfo === null" class="container">Chargement en cours...</p>
    <div v-else class="offer">
      <div class="left">
        <img :src="offerInfo.attributes.pictures.data[0].attributes.url" />
        <h1>{{ offerInfo.attributes.title }}</h1>
        <p>{{ offerInfo.attributes.price }} €</p>
        <p class="date">{{ formatDate }}</p>
        <h2>Description</h2>
        <p>{{ offerInfo.attributes.description }}</p>
        <p class="city">
          <font-awesome-icon :icon="['fas', 'map-marker-alt']" />Agon-Coutainville (50230)
        </p>
      </div>

      <div class="right">
        <div class="owner">
          <div>
            <img
              :src="offerInfo.attributes.owner.data.attributes.avatar.data.attributes.url"
              alt=""
            />
            <p>{{ offerInfo.attributes.owner.data.attributes.username }}</p>
          </div>

          <p class="identity">
            <font-awesome-icon :icon="['fas', 'check-double']" />Carte d'identitée vérifiée
          </p>
          <p><font-awesome-icon :icon="['far', 'clock']" />Répond généralement en 1 heure</p>
        </div>
        <div>
          <button>Acheter</button>
          <button>Message</button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.container {
  padding: 30px 0;
}

.offer {
  display: flex;
  gap: 20px;
}

.left {
  width: 67%;
}
h1 {
  font-size: 24px;
  font-weight: bold;
  margin: 30px 0;
}
h1 + p {
  font-size: 18px;
  font-weight: bold;
}

.date {
  font-size: 12px;
  color: var(--grey);
  margin-top: 20px;
}
h2 {
  border-top: 1px solid var(--grey-med);
  font-size: 18px;
  border-width: bold;
  margin: 50px 0 25px 0;
  padding-top: 20px;
  font-weight: bold;
}
.left img {
  width: 100%;
  height: 350px;
  object-fit: contain;
}
.left > div {
  position: relative;
}
.left > div svg {
  cursor: pointer;
  position: absolute;
  top: 50%;
}
.left svg:first-child {
  left: 10px;
}
.left svg:last-child {
  right: 10px;
}
.city {
  border-top: 1px solid var(--grey-med);
  margin: 50px 0 25px 0;
  padding-top: 20px;
}

.right {
  width: 33%;
  height: 375px;
  box-shadow: 0 0 5px var(--grey-med);
  border-radius: 2px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.right img {
  height: 65px;
  width: 65px;
  border-radius: 50%;
  object-fit: cover;
}
.owner {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.owner > div {
  display: flex;
  gap: 15px;
}
.owner > div p {
  font-weight: bold;
  text-transform: uppercase;
  font-size: 18px;
}
.identity {
  font-size: 12px;
  color: var(--brown);
  background-color: var(--orange-pale);
  border-radius: 10px;
  padding: 4px 7px;
  align-self: flex-start;
  margin-bottom: 20px;
}
.identity + p {
  font-size: 14px;
}

svg {
  margin-right: 3px;
}
.right > div:last-child {
  margin-top: 15px;
  padding: 15px 0;
  border-top: 1px solid var(--grey-med);
  display: flex;
  flex-direction: column;
  gap: 10px;
}
button {
  border: none;
  color: white;
  padding: 15px;
  border-radius: 15px;
  font-weight: bold;
}
button:first-child {
  background-color: var(--orange);
}
button:last-child {
  background-color: var(--blue-dark);
}
</style>
