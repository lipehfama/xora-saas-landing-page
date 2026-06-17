<script setup lang="ts">
import Marker from "./Marker.vue";

defineProps<{
  icon?: string;
  href?: string;
  containerClassName?: string;
  markerFill?: string;
}>();

defineEmits<{
  click: [];
}>();
</script>

<template>
  <component
    :is="href ? 'a' : 'button'"
    :href="href"
    class="g5 group relative rounded-2xl p-0.5 shadow-500"
    :class="containerClassName"
    @click="$emit('click')"
  >
    <span
      class="g4 inner-before relative flex min-h-[60px] items-center overflow-hidden rounded-2xl px-4 group-hover:before:opacity-100"
    >
      <span class="absolute -left-[1px]">
        <Marker :fill="markerFill" />
      </span>

      <img
        v-if="icon"
        :src="icon"
        alt="circle"
        class="z-10 mr-5 size-10 object-contain"
      />

      <span class="base-bold relative z-2 font-poppins uppercase text-p1">
        <slot />
      </span>

      <span class="glow-before glow-after" />
    </span>
  </component>
</template>
