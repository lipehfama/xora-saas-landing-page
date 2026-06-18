<script setup lang="ts">
import { ref, watch } from "vue";
import { plans } from "@/constants";
import PricingCard from "@/components/PricingCard.vue";
import bgOutlines from "@/assets/images/bg-outlines.svg";
import bgOutlinesFill from "@/assets/images/bg-outlines-fill.png";

const monthly = ref(false);

watch(monthly, (value) => {
  console.log("monthly:", value);
});
</script>
<template>
  <section id="pricing">
    <div class="container">
      <article
        class="pricing-head_before relative mx-auto max-w-960 border-l border-r border-s2 bg-s1/50 pb-40 pt-28 max-xl:max-w-4xl max-lg:border-none max-md:pb-32 max-md:pt-16"
      >
        <h3
          class="h3 max-lg:h4 max-md:h5 z-3 relative mx-auto mb-14 max-w-lg text-center text-p4 max-md:mb-11 max-sm:max-w-sm"
        >
          Flexible pricing for teams of all sizes.
        </h3>
        <div
          class="relative z-4 mx-auto flex w-[375px] rounded-3xl border-[3px] border-s4/25 bg-s1/50 p-2 backdrop-blur-[6px] max-md:w-[310px]"
        >
          <button
            class="pricing-head_btn cursor-pointer"
            :class="monthly && 'text-p4'"
            @click="monthly = true"
          >
            Monthly
          </button>

          <button
            class="pricing-head_btn cursor-pointer"
            :class="!monthly && 'text-p4'"
            @click="monthly = false"
          >
            Annual
          </button>
          <div
            class="g4 pricing-head_btn_before absolute left-2 top-2 h-[calc(100%_-_16px)] w-[calc(50%_-_8px)] overflow-hidden rounded-14 shadow-400 transition-transform duration-500 before:h-100"
            :class="!monthly && 'translate-x-full'"
          />
        </div>
        <figure class="pricing-bg">
          <img
            :src="bgOutlines"
            width="960"
            height="380"
            alt="outlines"
            class="relative z-2"
          />

          <img
            :src="bgOutlinesFill"
            width="960"
            height="380"
            alt="outlines fill"
            class="absolute inset-0 opacity-5 mix-blend-soft-light"
          />
        </figure>
      </article>
      <article
        class="scroll-hide relative z-2 -mt-12 flex items-start max-xl:gap-5 max-xl:overflow-auto max-xl:pt-6"
      >
        <PricingCard
          v-for="(plan, index) in plans"
          :key="plan.id"
          :plan="plan"
          :is-primary-plan="index === 1"
          :monthly="monthly"
        />
      </article>
    </div>
  </section>
</template>
