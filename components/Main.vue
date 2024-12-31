<template>
  <main class="p-4">
    <h1 class="text-2xl font-bold text-gray-800 mb-4">{{ blogContent?.Title || "Blog Content" }}</h1>

    <section v-if="!blogContent" class="mb-6">
      <p class="text-red-500">Error loading content.</p>
    </section>

    <section v-else>
      <section class="mb-6">
        <h2 class="text-xl font-semibold text-gray-700">Description</h2>
        <div class="prose prose-gray" v-html="blogContent.Desc"></div>
      </section>

      <section class="mb-6">
        <h2 class="text-xl font-semibold text-gray-700">Details</h2>
        <p><strong>Category:</strong> {{ blogContent.Category }}</p>
        <p><strong>Created Date:</strong> {{ new Date(blogContent.CreatedDate).toLocaleDateString() }}</p>
        <p><strong>Updated Date:</strong> {{ new Date(blogContent.UpdatedDate).toLocaleDateString() }}</p>
        <p><strong>Visit Statistics:</strong> {{ blogContent.VisitStatictics }}</p>
      </section>

      <section class="mb-6">
        <h2 class="text-xl font-semibold text-gray-700">Images</h2>
        <div class="flex space-x-4">
          <img :src="blogContent.Image" alt="Main" width="300" height="200" class="rounded-lg shadow" />
          <img :src="blogContent.ImageMedium" alt="Medium" width="300" height="200" class="rounded-lg shadow" />
          <img :src="blogContent.ImageThumbnail" alt="Thumbnail" width="300" height="200" class="rounded-lg shadow" />
        </div>
      </section>

      <section class="mb-6">
        <h2 class="text-xl font-semibold text-gray-700">Related Products</h2>
        <div v-for="(relatedProduct, index) in blogContent.RelatedProducts" :key="index" class="mb-4">
          <h3 class="text-lg font-medium text-gray-600">Carousel Group: {{ relatedProduct.CarouselGroup }}</h3>
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 mt-2">
            <div v-for="(product, idx) in relatedProduct.postProduct" :key="idx"
              class="p-4 border rounded-lg shadow hover:shadow-lg transition">
              <img :src="product.ImagePath" :alt="product.Name" width="300" height="200"
                class="object-cover rounded mb-2" />
              <h4 class="font-bold text-gray-800">{{ product.Name }}</h4>
              <p class="text-sm text-gray-600">Price: {{ product.Price || "N/A" }}</p>
              <p v-if="product.OldPrice" class="text-sm text-gray-500 line-through">Old Price: {{ product.OldPrice }}
              </p>
              <a :href="product.ProductUrl" class="text-blue-600 hover:underline text-sm" target="_blank"
                rel="noopener noreferrer">
                View Product
              </a>
            </div>
          </div>
        </div>
      </section>
    </section>
  </main>
</template>

<script setup>
import { useAsyncData } from '#app';

const API_URL = "https://api.gholab.ir/api/Blog/Home/هزینه-رجیستری-گوشی";

const { data, error } = await useAsyncData('blogData', () =>
  $fetch(API_URL, {
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json',
    }
  })
);

const blogContent = data.value || null;
</script>

<style scoped></style>