<script setup lang="ts">
import { useCategoryStore } from '@/stores/categories.store';
import { useBookmarkStore } from '@/stores/bookmark.store';
import { ref, watch, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import CategoryHeader from '@/components/CategoryHeader.vue';
import BookmarkCard from '@/components/BookmarkCard.vue';

const route = useRoute();
const categoryStore = useCategoryStore();
const bookmarkStore = useBookmarkStore();
const category = ref<Category>();

onMounted(() => {
  category.value = categoryStore.getCategoryByAlias(route.params.alias);
  if (category.value) {
    bookmarkStore.fetchBookmarks(category.value.id);
  }
});

watch(
  () => ({
    alias: route.params.alias,
    categories: categoryStore.categories,
  }),
  (data) => {
    category.value = categoryStore.getCategoryByAlias(data.alias);
    if (category.value) {
      bookmarkStore.fetchBookmarks(category.value.id);
    }
  },
);
</script>

<template>
  <CategoryHeader v-if="category" :category="category" />
  <BookmarkCard
    id="1"
    image="/public/avatar.png"
    title="GitHub - gofiber/fiber: ⚡️ Express inspired web framework written in Go"
    url="https://music.youtube.com/"
    :category-id="1"
    :created-at="new Date()"
  />
</template>
