<script setup lang="ts">
import ScrollAreaStory from "./_ScrollAreaStory.vue";
import ScrollAreaCopy from "./_ScrollAreaCopy.vue";
</script>

<template>
  <Story
    title="Scroll Area/Chromatic/Both"
    :layout="{ type: 'grid', width: '50%' }"
  >
    <Variant auto-props-disabled title="Both (Auto with overflow)">
      <ScrollAreaStory :type="'auto'" vertical horizontal>
        <ScrollAreaCopy v-for="i in 10" :key="i"></ScrollAreaCopy>
      </ScrollAreaStory>
    </Variant>

    <Variant auto-props-disabled title="Both (Auto without overflow)">
      <ScrollAreaStory :type="'auto'" vertical horizontal>
        <ScrollAreaCopy
          class="overflow-hidden !w-[50px] !h-[50px]"
        ></ScrollAreaCopy>
      </ScrollAreaStory>
    </Variant>

    <Variant auto-props-disabled title="Both (Always with overflow)">
      <ScrollAreaStory :type="'always'" vertical horizontal>
        <ScrollAreaCopy v-for="i in 10" :key="i"></ScrollAreaCopy>
      </ScrollAreaStory>
    </Variant>

    <Variant></Variant>

    <Variant auto-props-disabled title="Both (Scroll with overflow)">
      <ScrollAreaStory :type="'scroll'" vertical horizontal>
        <ScrollAreaCopy v-for="i in 10" :key="i"></ScrollAreaCopy>
      </ScrollAreaStory>
    </Variant>

    <Variant auto-props-disabled title="Both (Scroll without overflow)">
      <ScrollAreaStory :type="'scroll'" vertical horizontal>
        <ScrollAreaCopy
          class="overflow-hidden !w-[50px] !h-[50px]"
        ></ScrollAreaCopy>
      </ScrollAreaStory>
    </Variant>

    <Variant auto-props-disabled title="Both (Hover with overflow)">
      <ScrollAreaStory :type="'hover'" vertical horizontal>
        <ScrollAreaCopy v-for="i in 10" :key="i"></ScrollAreaCopy>
      </ScrollAreaStory>
    </Variant>

    <Variant auto-props-disabled title="Both (Hover without overflow)">
      <ScrollAreaStory :type="'hover'" vertical horizontal>
        <ScrollAreaCopy
          class="overflow-hidden !w-[50px] !h-[50px]"
        ></ScrollAreaCopy>
      </ScrollAreaStory>
    </Variant>
  </Story>
</template>
