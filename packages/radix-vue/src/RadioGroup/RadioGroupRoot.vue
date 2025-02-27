<script lang="ts">
import {
  PrimitiveDiv,
  usePrimitiveElement,
  type PrimitiveProps,
} from "@/Primitive";
import type { DataOrientation, Direction } from "@/shared/types";
import { useVModel } from "@vueuse/core";
import type { ComputedRef, Ref } from "vue";

export interface RadioGroupRootProps extends PrimitiveProps {
  modelValue?: string | string[];
  onValueChange?: (value: string) => void;
  defaultValue?: string;
  value?: string;
  disabled?: boolean;
  name?: string;
  required?: boolean;
  orientation?: DataOrientation;
  dir?: Direction;
  loop?: boolean;
}

export const RADIO_GROUP_INJECTION_KEY = "RadioGroup" as const;

export interface RadioGroupProvideValue {
  modelValue?: Readonly<Ref<string | string[] | undefined>>;
  changeModelValue: (value?: string) => void;
  parentElement: Ref<HTMLElement | undefined>;
  currentFocusedElement?: Ref<HTMLElement | undefined>;
  disabled: Ref<boolean>;
  loop: Ref<boolean>;
  orientation: Ref<DataOrientation | undefined>;
  name?: string;
  required: Ref<boolean>;
}

export const RADIO_ITEM_INJECTION_KEY = Symbol();

export interface RadioItemProvideValue {
  disabled: ComputedRef<boolean>;
  checked: ComputedRef<boolean>;
}
</script>

<script setup lang="ts">
import { provide, ref } from "vue";

const props = withDefaults(defineProps<RadioGroupRootProps>(), {
  disabled: false,
  required: false,
  orientation: undefined,
  dir: "ltr",
  loop: true,
});

const emits = defineEmits(["update:modelValue"]);

const { primitiveElement, currentElement: parentElement } =
  usePrimitiveElement();

const modelValue = useVModel(props, "modelValue", emits, {
  defaultValue: props.defaultValue,
  passive: true,
});

provide<RadioGroupProvideValue>(RADIO_GROUP_INJECTION_KEY, {
  modelValue,
  changeModelValue: (value?: string) => {
    modelValue.value = value;
    if (value && props.onValueChange) {
      props.onValueChange(value);
    }
  },
  parentElement,
  currentFocusedElement: ref(),
  disabled: ref(props.disabled),
  loop: ref(props.loop),
  orientation: ref(props.orientation),
  name: props.name,
  required: ref(props.required),
});
</script>

<template>
  <PrimitiveDiv
    ref="primitiveElement"
    role="radiogroup"
    :data-disabled="props.disabled ? '' : undefined"
    :as-child="props.asChild"
    :required="props.required"
    :aria-required="props.required"
    :dir="props.dir"
    :name="props.name"
  >
    <slot />
  </PrimitiveDiv>
</template>
