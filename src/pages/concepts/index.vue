<template>
  <HorizontalContainer>
    <Hero
      title="Nix concepts"
      description="The whys and the hows of Nix"
      client:none
    />

    <Grid3>
      <HoverableLink
        v-for="(page, idx) in conceptPages"
        :key="idx"
        :href="page.href"
        :text="page.frontmatter.title"
        size="normal"
      />
    </Grid3>
  </HorizontalContainer>
</template>

<script setup lang="ts">
import { conceptPages } from "../../logic/content";
</script>
