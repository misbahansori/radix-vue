<script lang="ts">
export interface AvatarFallbackProps extends PrimitiveProps {
  delayMs?: number;
}
</script>

<script setup lang="ts">
import { inject, ref } from "vue";
import {
  AVATAR_INJECTION_KEY,
  type AvatarProvideValue,
} from "./AvatarRoot.vue";
import { PrimitiveSpan, type PrimitiveProps } from "../Primitive";

const injectedValue = inject<AvatarProvideValue>(AVATAR_INJECTION_KEY);

const props = withDefaults(defineProps<AvatarFallbackProps>(), {
  delayMs: 0,
});

let canRender = ref(false);
let timeout: ReturnType<typeof setTimeout> | undefined;

if (props.delayMs) {
  timeout = setTimeout(() => {
    canRender.value = true;
    clearTimeout(timeout);
  }, props.delayMs);
} else {
  canRender.value = true;
}
</script>

<template>
  <PrimitiveSpan
    v-if="canRender && injectedValue?.imageLoadingStatus.value !== 'loaded'"
    :as-child="props.asChild"
  >
    <slot />
  </PrimitiveSpan>
</template>
