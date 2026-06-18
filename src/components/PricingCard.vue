<script setup lang="ts">
import { ref, computed, watch } from "vue";
import Button from "@/components/Button.vue";
import { plans } from "@/constants";
import checkIcon from "@/assets/images/check.png";

const props = defineProps<{
  plan: (typeof plans)[number];
  isPrimaryPlan: boolean;
  monthly: boolean;
}>();

const price = computed(() => {
  return props.monthly ? props.plan.priceMonthly : props.plan.priceYearly;
});

const animatedPrice = ref<number>(price.value);

watch(price, (newPrice, oldPrice) => {
  const duration = 400;
  const startTime = performance.now();

  function animatePrice(currentTime: number) {
    const elapsed = currentTime - startTime;
    const progress = Math.min(elapsed / duration, 1);

    animatedPrice.value = Math.round(
      oldPrice + (newPrice - oldPrice) * progress,
    );

    if (progress < 1) {
      requestAnimationFrame(animatePrice);
    }
  }
  requestAnimationFrame(animatePrice);
});
</script>

<template>
  <article
    class="pricing-plan_first pricing-plan_last pricing-plan_odd pricing-plan_even relative border-2 p-7 max-xl:min-w-80 max-lg:rounded-3xl xl:w-[calc(33.33%_+_2px)]"
  >
    <div
      v-if="isPrimaryPlan"
      class="g4 absolute left-0 right-0 top-0 z-1 h-330 rounded-tl-3xl rounded-tr-3xl"
    />
    <figure
      class="absolute left-0 right-0 z-2 flex items-center justify-center"
      :class="isPrimaryPlan ? '-top-6' : '-top-6 xl:-top-11'"
    >
      <img
        :src="plan.logo"
        :alt="`${plan.title} plan`"
        class="object-contain drop-shadow-2xl"
        :class="isPrimaryPlan ? 'size-[120px]' : 'size-[88px]'"
      />
    </figure>
    <header
      class="relative flex flex-col items-center"
      :class="isPrimaryPlan ? 'pt-24' : 'pt-12'"
    >
      <div
        class="small-2 relative z-2 mx-auto mb-6 rounded-20 border-2 px-4 py-1.5 uppercase"
        :class="isPrimaryPlan ? 'border-p3 text-p3' : 'border-p1 text-p1'"
      >
        {{ plan.title }}
      </div>

      <div class="relative z-2 flex items-center justify-center">
        <p
          class="h-num flex items-start"
          :class="isPrimaryPlan ? 'text-p3' : 'text-p4'"
        >
          ${{ animatedPrice }}
        </p>

        <p class="small-1 relative top-3 ml-1 uppercase">/ mo</p>
      </div>
    </header>

    <p
      class="body-1 relative z-2 mb-10 w-full border-b-s2 pb-9 text-center text-p4"
      :class="isPrimaryPlan && 'border-b'"
    >
      {{ plan.caption }}
    </p>

    <ul class="mx-auto space-y-4 xl:px-7">
      <li
        v-for="feature in plan.features"
        :key="`${plan.title}-${feature}`"
        class="relative flex items-center gap-5"
      >
        <img :src="checkIcon" alt="check icon" class="size-10 object-contain" />

        <p class="flex-1">
          {{ feature }}
        </p>
      </li>
    </ul>

    <aside class="mt-10 flex w-full justify-center">
      <Button :icon="plan.icon"> Get Started </Button>
    </aside>

    <p
      v-if="isPrimaryPlan"
      class="small-compact mt-9 text-center text-p3 before:mx-2.5 before:content-['-'] after:mx-2.5 after:content-['-']"
    >
      Limited time offer
    </p>
  </article>
</template>
