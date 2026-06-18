<script setup lang="ts">
import { socials, site_links } from "@/constants";
</script>

<template>
  <footer>
    <div class="container py-10">
      <section
        class="small-compact flex w-full items-center max-md:flex-col"
        aria-label="Footer"
      >
        <p class="flex flex-1 justify-center gap-5 opacity-70">
          &copy; Copyright, Xora
        </p>

        <nav
          class="flex items-center justify-center max-md:mt-4 sm:ml-auto"
          aria-label="Legal"
        >
          <a
            href="#"
            class="legal-after relative mr-9 text-p5 transition-all duration-500 hover:text-p1"
          >
            Privacy Policy
          </a>

          <a
            href="#"
            class="legal-after relative mr-9 text-p5 transition-all duration-500 hover:text-p1"
          >
            Terms of Use
          </a>

          <a
            :href="site_links.sourceCode"
            target="_blank"
            rel="noreferrer noopener"
            class="text-p5 transition-all duration-500 hover:text-p1"
          >
            Source Code
          </a>
        </nav>

        <ul
          class="flex flex-1 justify-center gap-3 max-md:mt-10 md:justify-end"
          aria-label="Social links"
        >
          <li v-for="social in socials" :key="social.id">
            <a
              :href="social.url"
              :aria-label="social.title"
              class="social-icon"
            >
              <img
                :src="social.icon"
                alt="social icons"
                class="size-1/3 object-contain"
              />
            </a>
          </li>
        </ul>
      </section>
    </div>
  </footer>
</template>
