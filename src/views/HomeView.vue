<script setup lang="ts">
import Card from '@/components/Card/index.vue';
import { ref, watch } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import cardsData from '../../cards.json'

const cards = ref(cardsData);
const expandedCardId = ref<number | null>(null);
const route = useRoute();
const router = useRouter();


const toggleCard = (id: number) => {
  if (expandedCardId.value === id) {
    expandedCardId.value = null
    router.replace({ query: {} })
  } else {
    expandedCardId.value = id
    router.replace({ query: { expanded: id } })
  }
}

watch(
  () => route.query.expanded,
  (newVal) => {
    if (typeof newVal === 'string') {
      const id = parseInt(newVal)
      expandedCardId.value = isNaN(id) ? null : id;
    } else {
      expandedCardId.value = null;
    }
  },
  { immediate: true }
)

</script>

<template>
  <main>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-2.5 grid-flow-row-dense p-5">
      <Card v-for="card in cards" :key="card.id" @click="toggleCard(card.id)" :expandedCardId="expandedCardId"
        :card="card" />
    </div>
  </main>
</template>
