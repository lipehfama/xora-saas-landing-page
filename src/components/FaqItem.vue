<script setup lang="ts">
import { computed, ref } from "vue";

const props = defineProps<{
  id: string;
  question: string;
  answer: string;
  index: number;
}>();

const active = ref(false);
const buttonId = computed(() => `faq-button-${props.id}`);
const answerId = computed(() => `faq-answer-${props.id}`);
</script>

<template>
  <article class="relative z-2 mb-16">
    <button
      :id="buttonId"
      type="button"
      class="group relative flex w-full cursor-pointer items-center justify-between gap-10 px-7 text-left"
      :aria-expanded="active"
      :aria-controls="answerId"
      @click="active = !active"
    >
      <div class="flex-1">
        <p class="small-compact mb-1.5 text-p3 max-lg:hidden">
          {{ index < 10 ? "0" : "" }}{{ index }}
        </p>

        <h4
          class="h-6 text-p4 transition-colors duration-500 max-md:flex max-md:min-h-20 max-md:items-center"
          :class="active && 'max-lg:text-p1'"
        >
          {{ question }}
        </h4>
      </div>

      <span
        class="faq-icon relative flex size-12 items-center justify-center rounded-full border-2 border-s2 shadow-400 transition-all duration-500 group-hover:border-s4"
        :class="active && 'before:bg-p1 after:rotate-0 after:bg-p1'"
        aria-hidden="true"
      >
        <span class="g4 size-11/12 rounded-full shadow-300" />
      </span>
    </button>

    <aside
      :id="answerId"
      role="region"
      :aria-labelledby="buttonId"
      class="overflow-hidden transition-all duration-300"
      :class="active ? 'max-h-40 opacity-100' : 'max-h-0 opacity-0'"
    >
      <p class="body-3 px-7 py-3.5">
        {{ answer }}
      </p>
    </aside>

    <aside
      class="g5 absolute -bottom-7 -top-7 left-0 right-0 -z-1 rounded-3xl opacity-0 transition-opacity duration-500"
      :class="active && 'opacity-100'"
    >
      <div class="g4 absolute inset-0.5 -z-1 rounded-3xl" />
      <div class="absolute left-8 top-0 h-0.5 w-40 bg-p1" />
    </aside>
  </article>
</template>
