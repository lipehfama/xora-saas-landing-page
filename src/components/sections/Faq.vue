<script setup lang="ts">
import FaqItem from "@/components/FaqItem.vue";
import { faq } from "@/constants";
import faqLogo from "@/assets/images/faq-logo.svg";

const halfLength = Math.floor(faq.length / 2);

const firstColumn = faq.slice(0, halfLength);
const secondColumn = faq.slice(halfLength);
</script>

<template>
  <section id="faq" class="relative">
    <article class="container relative z-2 py-28">
      <aside>
        <h3 class="h3 max-md:h5 mb-7 max-w-640 text-p4 max-lg:max-w-md">
          Curiosity didn&apos;t kill the cat, it gave it answers.
        </h3>

        <p class="body-1 max-lg:max-w-sm">
          You&apos;ve got questions, we&apos;ve got answers.
        </p>
      </aside>

      <div
        class="faq-line_after absolute left-[calc(50%_-_1px)] top-0 -z-1 h-full w-0.5 bg-s2"
      />
    </article>

    <article class="faq-glow_before relative z-2 border-2 border-s2 bg-s1">
      <div class="container flex gap-10 max-lg:block">
        <figure
          class="absolute -top-10 left-[calc(50%_-_40px)] z-4 flex size-20 items-center justify-center rounded-half border-2 border-s2 bg-s1"
        >
          <img :src="faqLogo" alt="logo" class="size-1/2" />
        </figure>

        <section class="relative flex-1 pt-24">
          <FaqItem
            v-for="(item, index) in firstColumn"
            :key="item.id"
            :id="item.id"
            :question="item.question"
            :answer="item.answer"
            :index="index + 1"
          />
        </section>

        <section class="relative flex-1 lg:pt-24">
          <FaqItem
            v-for="(item, index) in secondColumn"
            :key="item.id"
            :id="item.id"
            :question="item.question"
            :answer="item.answer"
            :index="halfLength + index + 1"
          />
        </section>
      </div>

      <div
        class="faq-line_after absolute left-[calc(50%_-_1px)] top-0 -z-1 h-full w-0.5 bg-s2 max-lg:hidden"
      />
    </article>
  </section>
</template>
