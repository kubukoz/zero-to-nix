<template>
  <section
    class="mb-6 rounded border-1.5 border-orange py-2 px-3.5 md:mb-8 md:py-3 md:px-5 lg:mb-10 lg:py-4 lg:px-6"
    v-if="showBanner"
  >
    <div class="flex items-center justify-between gap-4 md:gap-6 lg:gap-8">
      <p class="content text-dark dark:text-white md:text-lg lg:text-xl">
        We recommend starting with the
        <a href="/start">Nix quick start</a> and consulting concept docs like
        this for primarily for clarification. Feel free to click
        <strong>x</strong> to the right to disable this notification on
        <em>all</em> concept docs.
      </p>

      <button @click="disableBanner">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="h-4 w-4 stroke-2 text-orange hover:text-gray dark:text-orange dark:hover:text-primary md:h-5 md:w-5 lg:h-6 lg:w-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>
      </button>
    </div>
  </section>
</template>

<script setup lang="ts">
import { persistentAtom } from "@nanostores/persistent";
import { useStore } from "@nanostores/vue";
import { WritableAtom } from "nanostores";
import { onMounted, ref } from "vue";

const quickStartBannerAtom: WritableAtom<string> = persistentAtom<string>(
  "zero-to-nix:quick-start-banner",
  "open",
);

const quickStartBannerOpen: boolean =
  useStore(quickStartBannerAtom).value === "open";

const showBanner = ref<boolean>(false);

const disableBanner = () => {
  quickStartBannerAtom.set("closed");
  showBanner.value = false;
};

onMounted(() => {
  if (quickStartBannerOpen) {
    showBanner.value = true;
  }
});
</script>
