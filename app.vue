<template>
  <div>
    <Main />
  </div>
</template>

<script setup lang="ts">
useSeoMeta({
  title: 'My Amazing Site',
  ogTitle: 'My Amazing Site',
  description: 'This is my amazing site, let me tell you all about it.',
  ogDescription: 'This is my amazing site, let me tell you all about it.',
  ogImage: 'https://example.com/image.png',
  twitterCard: 'summary_large_image',
})
useHead({
  htmlAttrs: {
    lang: 'en',
    style: 'font-size: 13px'
  }
})
</script>

<style>
* {
  direction: rtl;
}

img {
  max-width: 100%;
}
</style>