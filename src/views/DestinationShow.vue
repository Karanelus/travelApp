<script setup>
import { computed, onMounted, ref, watch } from "vue";
import { useRoute } from "vue-router";
import SourceData from "../data.json";
import { getData } from "../components/api.ts";

const route = useRoute();
const destinationId = computed(() => route.params.id);
const destination = ref(null);

watch(
  () => route.params.slug,
  (newSlug) => {
    if (newSlug) {
      getData(newSlug).then((res) => (destination.value = res));
    }
  }
);
</script>

<template>
  <section v-if="destination" class="destination">
    <h2>{{ destination.name }}</h2>
    <div class="destination-details">
      <img :src="`/travel-app/images/${destination.image}`" :alt="destination.name" />
      <p>{{ destination.description }}</p>
    </div>
  </section>
</template>
