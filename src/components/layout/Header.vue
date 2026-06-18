<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";
import bgOutlines from "@/assets/images/bg-outlines.svg";
import bgOutlinesFill from "@/assets/images/bg-outlines-fill.png";
import closeIcon from "@/assets/images/close.svg";
import magicIcon from "@/assets/images/magic.svg";
import xoraLogo from "@/assets/images/xora.svg";

const hasScrolled = ref(false);
const isOpen = ref(false);
const activeSection = ref("");

const navButtonBaseClass =
  "base-bold max-lg:h5 cursor-pointer uppercase transition-colors duration-500 hover:text-p1 max-lg:my-4";

function navButtonClass(id: string) {
  return [
    navButtonBaseClass,
    activeSection.value === id ? "text-p3" : "text-p4",
  ];
}

function closeMenu() {
  isOpen.value = false;
}

function scrollToSection(id: string, offset = -100) {
  activeSection.value = id === "hero" ? "" : id;

  const section = document.getElementById(id);

  if (!section) return;

  const top = section.getBoundingClientRect().top + window.scrollY + offset;

  window.scrollTo({
    top,
    behavior: "smooth",
  });

  closeMenu();
}

function handleScroll() {
  hasScrolled.value = window.scrollY > 32;

  const hero = document.getElementById("hero");

  if (hero && hero.getBoundingClientRect().bottom > 140) {
    activeSection.value = "";
    return;
  }

  const sectionIds = ["features", "pricing", "faq", "download"] as const;
  let currentSection = "";

  for (let index = sectionIds.length - 1; index >= 0; index -= 1) {
    const id = sectionIds[index];
    const section = document.getElementById(id);

    if (!section) continue;

    if (section.getBoundingClientRect().top <= 140) {
      currentSection = id;
      break;
    }
  }

  if (currentSection) {
    activeSection.value = currentSection;
  }
}

onMounted(() => {
  handleScroll();
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
  <header
    class="fixed left-0 top-0 z-50 w-full transition-all duration-500"
    :class="
      hasScrolled
        ? 'bg-black-100 py-2 backdrop-blur-[8px] max-lg:py-2'
        : 'py-10 max-lg:py-4'
    "
  >
    <section class="container flex h-14 items-center max-lg:px-5">
      <figure class="z-2 flex-1 lg:hidden">
        <a
          href="#hero"
          class="block w-fit cursor-pointer"
          aria-label="Go to hero section"
          @click.prevent="scrollToSection('hero', -250)"
        >
          <img :src="xoraLogo" width="115" height="55" alt="Xora logo" />
        </a>
      </figure>

      <div
        id="primary-navigation"
        class="w-full max-lg:fixed max-lg:left-0 max-lg:top-0 max-lg:w-full max-lg:bg-s2 max-lg:opacity-0"
        :class="isOpen ? 'max-lg:opacity-100' : 'max-lg:pointer-events-none'"
      >
        <menu
          class="sidebar-before max-lg:relative max-lg:flex max-lg:min-h-screen max-lg:flex-col max-lg:overflow-hidden max-lg:p-6 max-md:px-4"
        >
          <nav
            class="max-lg:relative max-lg:z-2 max-lg:my-auto"
            aria-label="Primary navigation"
          >
            <ul class="flex max-lg:block max-lg:px-12">
              <li class="nav-li">
                <a
                  href="#features"
                  :class="navButtonClass('features')"
                  :aria-current="
                    activeSection === 'features' ? 'location' : undefined
                  "
                  @click.prevent="scrollToSection('features')"
                >
                  features
                </a>

                <div class="dot" aria-hidden="true" />

                <a
                  href="#pricing"
                  :class="navButtonClass('pricing')"
                  :aria-current="
                    activeSection === 'pricing' ? 'location' : undefined
                  "
                  @click.prevent="scrollToSection('pricing')"
                >
                  pricing
                </a>
              </li>

              <li class="nav-logo">
                <a
                  href="#hero"
                  class="cursor-pointer transition-transform duration-500 max-lg:hidden"
                  aria-label="Go to hero section"
                  @click.prevent="scrollToSection('hero', -250)"
                >
                  <img
                    :src="xoraLogo"
                    width="160"
                    height="55"
                    alt="Xora logo"
                  />
                </a>
              </li>

              <li class="nav-li">
                <a
                  href="#faq"
                  :class="navButtonClass('faq')"
                  :aria-current="
                    activeSection === 'faq' ? 'location' : undefined
                  "
                  @click.prevent="scrollToSection('faq')"
                >
                  faq
                </a>

                <div class="dot" aria-hidden="true" />

                <a
                  href="#download"
                  :class="navButtonClass('download')"
                  :aria-current="
                    activeSection === 'download' ? 'location' : undefined
                  "
                  @click.prevent="scrollToSection('download')"
                >
                  download
                </a>
              </li>
            </ul>
          </nav>

          <figure
            class="absolute left-0 top-1/2 block h-[380px] w-[960px] -translate-y-1/2 translate-x-[-290px] rotate-90 lg:hidden"
            aria-hidden="true"
          >
            <img
              :src="bgOutlines"
              alt="background outlines"
              width="960"
              height="380"
              class="relative z-2"
            />

            <img
              :src="bgOutlinesFill"
              alt="background outlines fill"
              width="960"
              height="380"
              class="absolute inset-0 opacity-5 mix-blend-soft-light"
            />
          </figure>
        </menu>
      </div>

      <button
        type="button"
        class="z-2 flex size-10 cursor-pointer items-center justify-center rounded-full border-2 border-s4/25 lg:hidden"
        :aria-expanded="isOpen"
        aria-controls="primary-navigation"
        :aria-label="isOpen ? 'Close menu' : 'Open menu'"
        @click="isOpen = !isOpen"
      >
        <img
          :src="isOpen ? closeIcon : magicIcon"
          alt=""
          class="size-1/2 object-contain"
        />
      </button>
    </section>
  </header>
</template>
