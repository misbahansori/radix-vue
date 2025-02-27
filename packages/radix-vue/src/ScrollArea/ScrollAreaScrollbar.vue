<script lang="ts">
import { type Ref } from "vue";
export interface ScrollAreaScrollbarProps extends PrimitiveProps {
  orientation: "vertical" | "horizontal";
  forceMount?: boolean;
}

export interface ScrollAreaScollbarProvideValue {
  orientation: Ref<"vertical" | "horizontal">;
  forceMount?: Ref<boolean>;
  isHorizontal: Ref<boolean>;
  asChild: Ref<boolean>;
}

export const SCROLL_AREA_SCROLLBAR_INJECTION_KEY =
  Symbol() as InjectionKey<ScrollAreaScollbarProvideValue>;

export default {
  inheritAttrs: false,
};
</script>

<script setup lang="ts">
import {
  computed,
  inject,
  onUnmounted,
  watch,
  provide,
  toRefs,
  type InjectionKey,
} from "vue";
import { SCROLL_AREA_INJECTION_KEY } from "./ScrollAreaRoot.vue";
import { type PrimitiveProps } from "@/Primitive";
import ScrollAreaScrollbarHover from "./ScrollAreaScrollbarHover.vue";
import ScrollAreaScrollbarScroll from "./ScrollAreaScrollbarScroll.vue";
import ScrollAreaScrollbarAuto from "./ScrollAreaScrollbarAuto.vue";
import ScrollAreaScrollbarVisible from "./ScrollAreaScrollbarVisible.vue";

const injectedValue = inject(SCROLL_AREA_INJECTION_KEY);

const props = withDefaults(defineProps<ScrollAreaScrollbarProps>(), {
  orientation: "vertical",
  forceMount: undefined,
});

const isHorizontal = computed(() => props.orientation === "horizontal");

watch(
  isHorizontal,
  () => {
    if (isHorizontal.value) {
      injectedValue?.onScrollbarXEnabledChange(true);
    } else {
      injectedValue?.onScrollbarYEnabledChange(true);
    }
  },
  { immediate: true }
);

onUnmounted(() => {
  injectedValue?.onScrollbarXEnabledChange(false);
  injectedValue?.onScrollbarYEnabledChange(false);
});

const { orientation, forceMount, asChild } = toRefs(props);
provide<ScrollAreaScollbarProvideValue>(SCROLL_AREA_SCROLLBAR_INJECTION_KEY, {
  orientation,
  forceMount,
  isHorizontal,
  asChild,
});
</script>

<template>
  <ScrollAreaScrollbarHover
    v-bind="$attrs"
    v-if="injectedValue?.type.value === 'hover'"
    :forceMount="forceMount"
  >
    <slot></slot>
  </ScrollAreaScrollbarHover>
  <ScrollAreaScrollbarScroll
    v-bind="$attrs"
    v-else-if="injectedValue?.type.value === 'scroll'"
    :forceMount="forceMount"
  >
    <slot></slot>
  </ScrollAreaScrollbarScroll>
  <ScrollAreaScrollbarAuto
    v-bind="$attrs"
    v-else-if="injectedValue?.type.value === 'auto'"
    :forceMount="forceMount"
  >
    <slot></slot>
  </ScrollAreaScrollbarAuto>
  <ScrollAreaScrollbarVisible
    v-bind="$attrs"
    data-state="visible"
    v-else-if="injectedValue?.type.value === 'always'"
    :forceMount="forceMount"
  >
    <slot></slot>
  </ScrollAreaScrollbarVisible>
</template>
