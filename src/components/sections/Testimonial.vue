<script setup lang="ts">
import TestimonialItem from "@/components/TestimonialItem.vue";
import { testimonials } from "@/constants";

const halfLength = Math.floor(testimonials.length / 2);

const firstColumn = testimonials.slice(0, halfLength);
const secondColumn = testimonials.slice(halfLength);
</script>

<template>
  <section class="relative z-2 py-24 md:py-28 lg:py-40">
    <article class="container block lg:flex">
      <aside
        class="testimonials_head-res relative z-2 mr-20 w-300 shrink-0 max-lg:w-auto"
      >
        <p class="caption mb-5 max-md:mb-2.5">Wall of Love</p>

        <h3 class="h3 max-w-300 max-md:h5 text-p4">Words from our fans</h3>
      </aside>

      <div
        class="testimonials_inner-after testimonials_inner-before relative -my-12 -mr-3 flex items-start max-lg:static max-md:block"
      >
        <section class="testimonials_group-after flex-50">
          <TestimonialItem
            v-for="testimonial in firstColumn"
            :key="testimonial.id"
            :avatar-url="testimonial.avatarUrl"
            :comment="testimonial.comment"
            :name="testimonial.name"
            :role="testimonial.role"
            container-class-name="last:after:hidden last:after:max-md:block"
          />
        </section>

        <section class="flex-50">
          <TestimonialItem
            v-for="testimonial in secondColumn"
            :key="testimonial.id"
            :avatar-url="testimonial.avatarUrl"
            :comment="testimonial.comment"
            :name="testimonial.name"
            :role="testimonial.role"
            container-class-name="last:after:hidden after:right-auto after:left-0 after:max-md:-left-4 md:px-12"
          />
        </section>
      </div>
    </article>
  </section>
</template>
