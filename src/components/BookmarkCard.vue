<script setup lang="ts">
import IconLinkWhite from '@/icons/IconLinkWhite.vue';
import IconTrashWhite from '@/icons/IconTrashWhite.vue';
import type { Bookmark } from '@/interfaces/bookmark.interface';
import ButtonIconBig from './ButtonIconBig.vue';
import { useBookmarkStore } from '@/stores/bookmark.store';
import { ref } from 'vue';
import PopupConfirm from './PopupConfirm.vue';

const { title, image, url, id, category_id } = defineProps<Bookmark>();
const bookmarkStore = useBookmarkStore();
const isOpened = ref<boolean>(false);

function openLink() {
  window.open(url, '_blank');
}

function deleteBookmark() {
  isOpened.value = !isOpened.value;
  bookmarkStore.deleteBookmark(id, category_id);
}
</script>

<template>
  <div class="bookmark-card">
    <div class="bookmark-card__image" :style="{ backgroundImage: `url(${image})` }"></div>
    <div class="bookmark-card__title">
      {{ title }}
    </div>
    <div class="bookmark-card__footer">
      <ButtonIconBig @click="isOpened = !isOpened">
        <IconTrashWhite />
      </ButtonIconBig>
      <ButtonIconBig @click="openLink">
        <IconLinkWhite />
      </ButtonIconBig>
      <PopupConfirm
        text="Хотите удалить закладку?"
        :is-opened="isOpened"
        @cancel="isOpened = !isOpened"
        @ok="deleteBookmark"
      />
    </div>
  </div>
</template>

<style scoped>
.bookmark-card {
  border-radius: 30px;
  background: var(--color-fg);
  box-shadow: 0px 10px 10px 0px rgba(245, 245, 247, 0.1);
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 24px;
}
.bookmark-card__image {
  min-height: 160px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  border-radius: 20px;
}
.bookmark-card__title {
  font-size: 16px;
  font-weight: 500;
  color: var(--color-bg);
}
.bookmark-card__footer {
  display: flex;
  justify-content: space-between;
}
</style>
