<script setup lang="ts">
import Marker from "@/components/Marker.vue";
import { links, logos } from "@/constants";
import lines from "@/assets/images/lines.svg";
import screen from "@/assets/images/screen.jpg";
import xoraLogo from "@/assets/images/xora.svg";
</script>

<template>
  <section
    id="download"
    class="g7 relative pb-32 pt-24 max-lg:pb-24 max-md:py-16"
  >
    <div class="container">
      <section class="flex items-center">
        <article
          class="relative mr-6 flex-[0_0_540px] max-xl:flex-[0_0_280px] max-lg:flex-[0_0_256px] max-md:flex-[0_0_100%]"
        >
          <header class="mb-10">
            <img :src="xoraLogo" width="160" height="55" alt="Xora logo" />
          </header>

          <p class="body-1 mb-10 max-w-md">
            Try it now for free on iOS, Android, PC, Web - whatever your
            flavour, we&apos;ve got you covered.
          </p>

          <nav aria-label="Download platforms">
            <ul class="flex flex-wrap items-center gap-6">
              <li
                v-for="link in links"
                :key="link.id"
                class="download_tech-link download_tech-link_last-before download_tech-link_last-after"
              >
                <a
                  :href="link.url"
                  :aria-label="`Download for ${link.title}`"
                  class="download_tech-icon_before relative flex size-22 items-center justify-center rounded-half border-2 border-s3 bg-s1 transition-borderColor duration-500"
                >
                  <span class="absolute -top-2 rotate-90" aria-hidden="true">
                    <Marker />
                  </span>

                  <img
                    :src="lines"
                    alt=""
                    class="absolute size-13/20 object-contain"
                  />

                  <span class="download_tech-icon" v-html="link.icon" />
                </a>
              </li>
            </ul>
          </nav>
        </article>

        <figure class="mb-10 max-md:hidden">
          <div
            class="download_preview-before download_preview-after relative w-[955px] rounded-40 border-2 border-s5 p-6"
          >
            <div class="relative rounded-3xl bg-s1 px-6 pb-6 pt-14">
              <span
                class="download_preview-dot left-6 bg-p2"
                aria-hidden="true"
              />
              <span
                class="download_preview-dot left-11 bg-s3"
                aria-hidden="true"
              />
              <span
                class="download_preview-dot left-16 bg-p1/15"
                aria-hidden="true"
              />

              <img
                :src="screen"
                alt="Xora workflow dashboard preview"
                width="855"
                height="655"
                class="rounded-xl"
              />
            </div>
          </div>
        </figure>
      </section>

      <ul
        class="mt-24 flex justify-center max-lg:hidden"
        aria-label="Trusted by"
      >
        <li v-for="logo in logos" :key="logo.id" class="mx-10">
          <img
            :src="logo.url"
            :width="logo.width"
            :height="logo.height"
            :alt="logo.title"
          />
        </li>
      </ul>
    </div>
  </section>
</template>
