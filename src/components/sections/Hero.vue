<script setup lang="ts">
import Button from "../../components/Button.vue";
import zapIcon from "../../assets/images/zap.svg";
</script>

<template>
  <section
    class="relative pb-40 pt-60 max-lg:pb-36 max-lg:pt-52 max-md:pb-32 max-md:pt-36"
  >
    <div class="container">
      <article class="relative z-2 max-w-512 max-lg:max-w-388">
        <aside class="caption small-2 uppercase text-p3">Video Editing</aside>
        <h1
          class="h1 max-lg:h2 mb-6 uppercase text-p4 max-lg:mb-7 max-md:mb-4 max-md:text-5xl max-md:leading-12"
        >
          Amazingly simple
        </h1>

        <p class="body-1 mb-14 max-w-440 max-md:mb-10">
          We designed Xora AI Video Editor to be an easy to use, quick to learn,
          and surprisingly powerful.
        </p>
        <Button :icon="zapIcon">Try it now</Button>
      </article>
      <figure
        class="hero-img_res pointer-events-none absolute -top-32 left-[calc(50%_-_340px)] w-[1230px]"
      >
        <img
          src="../../assets/images/hero.png"
          alt="Hero"
          class="size-1230 max-lg:h-auto"
        />
      </figure>
    </div>
  </section>
</template>
