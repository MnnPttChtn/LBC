<script setup>
import { computed } from 'vue'
import { RouterLink } from 'vue-router'

const props = defineProps({
  offerInfos: {
    type: Object,
    required: true,
  },

  id: {
    type: Number,
    required: true,
  },
})

const formatDate = computed(() => {
  return props.offerInfos.updatedAt.split('T')[0].split('-').reverse().join('/')
})
</script>
<template>
  <RouterLink :to="{ name: 'offer', params: { id: id } }" class="card">
    <div class="top">
      <div class="owner">
        <img
          :src="offerInfos.owner.data.attributes.avatar.data.attributes.url"
          alt=""
          v-if="offerInfos.owner.data.attributes.avatar.data"
        />
        <p>{{ offerInfos.owner.data.attributes.username }}</p>
      </div>
      <img :src="offerInfos.pictures.data[0].attributes.url" alt="" />
      <p>{{ offerInfos.title }}</p>
      <p>{{ offerInfos.price }} €</p>
    </div>
    <div class="date">
      <div>
        <p>{{ formatDate }}</p>
      </div>
      <font-awesome-icon :icon="['far', 'heart']" />
    </div>
  </RouterLink>
</template>
<style scoped>
.card {
  height: 380px;
  width: calc((100% - 60px) / 5);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  text-decoration: none;
  color: black;
}
img {
  height: 25px;
  width: 25px;
  border-radius: 50%;
  object-fit: cover;
}

.top > img {
  height: 240px;
  width: 100%;
  border-radius: 10px;
  margin: 7px 0 5px 0;
}

.top p {
  font-weight: bold;
  line-height: 20px;
}
.top p:last-child {
  margin-top: 5px;
}
.owner {
  display: flex;
  align-items: center;
  gap: 5px;
}
.owner p {
  font-size: 14px;
}

.date {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}
.date p {
  color: var(--grey);
  font-size: 12px;
  line-height: 16px;
}
svg {
  font-size: 20px;
  color: var(--grey);
}
</style>
