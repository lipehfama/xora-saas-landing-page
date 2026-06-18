<script setup lang="ts">
import Button from "@/components/Button.vue";
import { features, details } from "@/constants";
</script>

<template>
  <section id="features">
    <div class="container">
      <article
        class="feature-after md:g7 relative flex flex-nowrap rounded-40 border-2 border-s3 max-md:flex-col max-md:gap-3 max-md:rounded-none max-md:border-none md:flex-wrap md:overflow-hidden"
      >
        <div
          v-for="feature in features"
          :key="feature.id"
          class="max-md:g7 relative z-2 flex-50 px-5 pb-5 max-md:flex-320 max-md:rounded-3xl max-md:border-2 max-md:border-s3 md:px-10 md:pb-10"
        >
          <section class="flex w-full items-start justify-start">
            <figure
              class="-ml-3 mb-12 flex flex-col items-center justify-center"
            >
              <div class="h-16 w-0.5 bg-s3" />
              <img
                :src="feature.icon"
                alt="feature.title"
                class="size-28 object-contain"
              />
            </figure>
          </section>
          <p class="caption mb-5 max-md:mb-6">
            {{ feature.caption }}
          </p>
          <h2 class="h3 max-md:h5 mb-7 max-w-400 text-p4 max-md:mb-6">
            {{ feature.title }}
          </h2>
          <p class="body-1 max-md:body-3 mb-11 max-md:mb-8">
            {{ feature.text }}
          </p>
          <Button :icon="feature.button.icon">
            {{ feature.button.title }}
          </Button>
        </div>
        <section class="relative grow max-md:hidden">
          <ul
            class="relative flex justify-around rounded-40 border-2 border-s3 px-[5%]"
          >
            <li
              v-for="detail in details"
              :key="detail.id"
              class="relative px-4 pb-14 pt-16"
            >
              <div
                class="absolute bottom-0 left-1/2 top-0 z-10 h-full w-px bg-s3/20"
              />
              <figure
                class="mx-auto mb-3 flex size-20 items-center justify-center rounded-full border-2 border-s2 shadow-500 transition-all duration-500 hover:border-s4"
              >
                <img
                  :src="detail.icon"
                  alt=""
                  class="z-20 size-17/20 object-contain"
                />
              </figure>
              <h3
                class="base-small relative z-2 mx-auto my-0 max-w-36 text-center uppercase"
              >
                {{ detail.title }}
              </h3>
            </li>
          </ul>
          <div
            class="absolute left-0 right-0 top-[38%] z-10 h-px w-full bg-s3/20"
            aria-hidden="true"
          />
        </section>
      </article>
    </div>
  </section>
</template>
