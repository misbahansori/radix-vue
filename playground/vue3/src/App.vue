<script setup lang="ts">
import Card from "./components/Card.vue";

import AccordionDemo from "./components/Demo/AccordionDemo.vue";
import CheckboxDemo from "./components/Demo/CheckboxDemo.vue";
import CollapsibleDemo from "./components/Demo/CollapsibleDemo.vue";
import LabelDemo from "./components/Demo/LabelDemo.vue";
import SeparatorDemo from "./components/Demo/SeparatorDemo.vue";
import SwitchDemo from "./components/Demo/SwitchDemo.vue";
import ToggleDemo from "./components/Demo/ToggleDemo.vue";
import ToggleGroupDemo from "./components/Demo/ToggleGroupDemo.vue";
import AspectRatioDemo from "./components/Demo/AspectRatioDemo.vue";
import TabsDemo from "./components/Demo/TabsDemo.vue";
import SliderDemo from "./components/Demo/SliderDemo.vue";
import ProgressDemo from "./components/Demo/ProgressDemo.vue";
import DialogDemo from "./components/Demo/DialogDemo.vue";
import AlertDialogDemo from "./components/Demo/AlertDialogDemo.vue";
import RadioGroupDemo from "./components/Demo/RadioGroupDemo.vue";
import ToolbarDemo from "./components/Demo/ToolbarDemo.vue";
import AvatarDemo from "./components/Demo/AvatarDemo.vue";
import TooltipDemo from "./components/Demo/TooltipDemo.vue";
import HoverCardDemo from "./components/Demo/HoverCardDemo.vue";
import PopoverDemo from "./components/Demo/PopoverDemo.vue";
import DropdownMenuDemo from "./components/Demo/DropdownMenuDemo.vue";
import ContextMenuDemo from "./components/Demo/ContextMenuDemo.vue";
import ScrollAreaDemo from "./components/Demo/ScrollAreaDemo.vue";
import SelectDemo from "./components/Demo/SelectDemo.vue";
import MenubarDemo from "./components/Demo/MenubarDemo.vue";
import SelectMultipleDemo from "./components/Demo/SelectMultipleDemo.vue";
import NavigationMenuDemo from "./components/Demo/NavigationMenuDemo.vue";
</script>

<template>
  <div class="w-full flex flex-col items-center">
    <div class="max-w-6xl w-full grid grid-cols-3 gap-4 pt-40 pb-40">
      <Card>
        <AccordionDemo />
      </Card>
      <Card>
        <AlertDialogDemo />
      </Card>
      <Card>
        <AspectRatioDemo />
      </Card>
      <Card>
        <AvatarDemo />
      </Card>
      <Card>
        <CheckboxDemo />
      </Card>
      <Card>
        <CollapsibleDemo />
      </Card>
      <Card>
        <ScrollAreaDemo />
      </Card>
      <Card class="col-span-2">
        <ContextMenuDemo />
      </Card>
      <Card class="col-span-2">
        <DialogDemo />
      </Card>
      <Card>
        <DropdownMenuDemo />
      </Card>
      <Card>
        <MenubarDemo />
      </Card>
      <Card class="col-span-2">
        <NavigationMenuDemo />
      </Card>
      <Card>
        <HoverCardDemo />
      </Card>
      <Card>
        <LabelDemo />
      </Card>
      <Card>
        <PopoverDemo />
      </Card>
      <Card>
        <ProgressDemo />
      </Card>
      <Card>
        <RadioGroupDemo />
      </Card>
      <Card>
        <SelectDemo />
      </Card>
      <Card>
        <SelectMultipleDemo />
      </Card>
      <Card>
        <SeparatorDemo />
      </Card>
      <Card>
        <SliderDemo />
      </Card>
      <Card>
        <SwitchDemo />
      </Card>
      <Card>
        <TabsDemo />
      </Card>
      <Card>
        <ToggleDemo />
      </Card>
      <Card>
        <ToggleGroupDemo />
      </Card>
      <Card class="col-span-2">
        <ToolbarDemo />
      </Card>
      <Card>
        <TooltipDemo />
      </Card>
    </div>
  </div>
</template>

<style>
body {
  @apply bg-black text-white;
}
</style>
