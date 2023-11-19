<template>
  <DefaultLayout />
</template>

<script setup>
  import DefaultLayout from '@/layouts/default/Default.vue';

  import { useLocale } from 'vuetify';
  const { current } = useLocale();
  current.value = 'ar'
</script>
