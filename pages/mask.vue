<script setup lang="ts">
</script>

<template>
  <div class="h-[40rem] w-full flex items-center justify-center  overflow-hidden">
    <MaskContainer
      class="h-[40rem] border rounded-md"
    >
    <template #revealText>
        <p class="max-w-4xl mx-auto text-slate-800 text-center  text-4xl font-bold">
          The first rule of MRR Club is you do not talk about MRR Club. The
          second rule of MRR Club is you DO NOT talk about MRR Club.
        </p>
      </template>
      The first rule of <span class="text-red-500">MRR Club</span> is you
      do not talk about MRR Club. The second rule of MRR Club is you DO NOT
      talk about <span class="text-red-500">MRR Club</span>.
    </MaskContainer>
  </div>
</template>