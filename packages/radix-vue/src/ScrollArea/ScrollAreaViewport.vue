<script setup lang="ts">
import { inject, onMounted, ref } from "vue";
import {
  PrimitiveDiv,
  usePrimitiveElement,
  type PrimitiveProps,
} from "@/Primitive";
import { SCROLL_AREA_INJECTION_KEY } from "./ScrollAreaRoot.vue";

interface ScrollAreaViewport extends PrimitiveProps {}
const props = defineProps<ScrollAreaViewport>();

const rootContext = inject(SCROLL_AREA_INJECTION_KEY);

const { primitiveElement, currentElement: contentElement } =
  usePrimitiveElement();

const viewportElement = ref<HTMLElement>();

onMounted(() => {
  rootContext?.onViewportChange(viewportElement.value!);
  rootContext?.onContentChange(contentElement.value!);
});
</script>

<template>
  <component :is="'style'">
    [data-radix-scroll-area-viewport] { scrollbar-width: none;
    -ms-overflow-style: none; -webkit-overflow-scrolling: touch; }
    [data-radix-scroll-area-viewport]::-webkit-scrollbar { display: none; }
  </component>
  <div
    ref="viewportElement"
    data-radix-scroll-area-viewport=""
    :style="{
      /**
       * We don't support `visible` because the intention is to have at least one scrollbar
       * if this component is used and `visible` will behave like `auto` in that case
       * https://developer.mozilla.org/en-US/docs/Web/CSS/overflowed#description
       *
       * We don't handle `auto` because the intention is for the native implementation
       * to be hidden if using this component. We just want to ensure the node is scrollable
       * so could have used either `scroll` or `auto` here. We picked `scroll` to prevent
       * the browser from having to work out whether to render native scrollbars or not,
       * we tell it to with the intention of hiding them in CSS.
       */
      overflowX: rootContext?.scrollbarXEnabled.value ? 'scroll' : 'hidden',
      overflowY: rootContext?.scrollbarYEnabled.value ? 'scroll' : 'hidden',
    }"
  >
    <PrimitiveDiv
      ref="primitiveElement"
      :style="{ minWidth: '100%', display: 'table' }"
      :as-child="props.asChild"
    >
      <slot></slot>
    </PrimitiveDiv>
  </div>
</template>
