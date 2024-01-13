<script setup lang="ts">
import { Motion, Presence, PresenceGroup, spring } from "@oku-ui/motion"

const { item, idx } = defineProps({
  idx: {
    type: Number,
    required: true,
  },
  item: {
    type: Object,
    required: true,
  },
})

const hovered = ref(null)
const x = ref(0)
const rotate = ref(0)
const motion = ref()

async function handleMouseMove(event) {
  const halfWidth = event.target.offsetWidth / 2;
  // await set({ translateX: x.value })
  x.value = event.offsetX - halfWidth
  rotate.value = x.value
  console.log(rotate.value)
}

</script>

<template>
         <div
          class="-mr-4  relative group"
          @mouseover="hovered = idx"
          @mouseleave="hovered = null"
        >
          <Presence>
              <Motion
              tag="div"
              :ref="motion"
              v-show="idx === hovered"
                :initial="{ opacity: 0, y: 20, scale: 0.6 }"
                :animate="{
                  opacity: 1,
                  y: 0,
                  x: x,
                  rotate: rotate,
                  scale: 1,
              
                }"
                :transition="{
                  easing: spring({
                    damping: 5,
                    stiffness: 100,
                  })
                }"
                :exit="{ opacity: 0, y: 20, scale: 0.6 }"
                :style="{
                  // translateX: x,
                  // rotate: rotate,
                  whiteSpace: 'nowrap',
                }"
                class="absolute -top-16 -left-1/2 translate-x-1/2 flex text-xs  flex-col items-center justify-center rounded-md bg-black z-50 shadow-xl px-4 py-2"
              >
                <div class="absolute inset-x-10 z-30 w-[20%] -bottom-px bg-gradient-to-r from-transparent via-emerald-500 to-transparent h-px " />
                <div class="absolute left-10 w-[40%] z-30 -bottom-px bg-gradient-to-r from-transparent via-sky-500 to-transparent h-px " />
                <div class="font-bold text-white relative z-30 text-base">
                  {{item.name}}
                </div>
                <div class="text-white text-xs">{{item.designation}}</div>
              </Motion>
          </Presence>
          <img
          @mousemove="handleMouseMove"
            :height="100"
            :width="100"
            :src="item.image"
            :alt="item.name"
            class="object-cover !m-0 !p-0 object-top rounded-full h-14 w-14 border-2 group-hover:scale-105 group-hover:z-30 border-white  relative transition duration-500"
          />
        </div>
</template>