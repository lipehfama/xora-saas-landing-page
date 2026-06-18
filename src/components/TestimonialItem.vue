<script setup lang="ts">
defineProps<{
  avatarUrl: string;
  comment: string;
  name: string;
  role: string;
  containerClassName?: string;
}>();
</script>

<template>
  <article
    class="relative px-14 pb-14 pt-11 after:absolute after:bottom-0 after:right-0 after:h-0.5 after:w-screen after:bg-s2 after:content-[''] max-md:px-0 max-md:pt-11 after:max-md:-right-4"
    :class="containerClassName"
  >
    <blockquote>
      <p class="h6 mb-8 text-p4">
        {{ comment }}
      </p>

      <footer class="flex items-center max-xl:mr-8">
        <figure
          class="mr-4 size-20 shrink-0 rounded-half border-2 border-s2 p-1.5"
        >
          <img
            :src="avatarUrl"
            :alt="`${name} portrait`"
            class="size-full object-cover"
          />
        </figure>

        <div>
          <cite class="body-2 mb-0.5 block not-italic text-p1">
            {{ name }}
          </cite>

          <p class="small-compact uppercase text-s3">
            {{ role }}
          </p>
        </div>
      </footer>
    </blockquote>
  </article>
</template>
