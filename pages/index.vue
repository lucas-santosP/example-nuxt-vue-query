<script setup lang="ts">
import { useQuery } from "@tanstack/vue-query";

const enabled = ref(false);

function toggleEnabled() {
  enabled.value = !enabled.value;
}

const fetcher = async () =>
  await fetch("https://jsonplaceholder.typicode.com/posts").then((response) => response.json());

const { data, suspense } = useQuery({ queryKey: ["test"], queryFn: fetcher, enabled: enabled });
await suspense();
</script>

<template>
  <button @click="toggleEnabled">toggle enabled</button>
  <p>
    {{ enabled }}
  </p>

  <div>{{ data }}</div>
</template>
