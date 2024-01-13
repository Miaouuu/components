<script setup lang="ts">
import { Motion } from "@oku-ui/motion"

const mousePosition = reactive({
    x: 0,
    y: 0,
})
const isHovered = ref(false)
const c = ref<VNode | null>(null)

  const updateMousePosition = (event: MouseEvent) => {
    const rect = c.value?.getBoundingClientRect()
    mousePosition.x = event.clientX - rect.left
    mousePosition.y = event.clientY - rect.top
    console.log(mousePosition.x, mousePosition.y)
  }

  const maskSize = computed(() => {
    return isHovered.value ? 600 : 10
  })
</script>

<template>
    <div
      ref="c"
        @mousemove="updateMousePosition"
        class="h-screen relative"
        :style="{
          backgroundColor: isHovered ? 'grey' : 'white',
        }"
      >
      <Motion
        class="w-full h-full flex items-center justify-center text-6xl absolute bg-black bg-grid-white/[0.2] text-white [mask-size:40px] [mask-repeat:no-repeat]"
        :animate="{
          maskPosition: `${mousePosition.x - maskSize / 2}px ${
            mousePosition.y - maskSize / 2
          }px`,
          maskImage: 'url(/components/mask.svg)',
          maskSize: `${maskSize}px`,
          transition: {
            duration: 0.1,
          },
        }"
      >
        <div class="absolute inset-0 bg-black h-full w-full z-0 opacity-50" />
        <div
          @mouseenter="isHovered = true"
          @mouseleave="isHovered = false"
          class="max-w-4xl mx-auto text-center text-white  text-4xl font-bold relative z-20"
        >
          <slot />
        </div>
      </Motion>

      <div class="w-full h-full flex items-center justify-center  text-white">
        <slot name="revealText" />
      </div>
    </div>
</template>