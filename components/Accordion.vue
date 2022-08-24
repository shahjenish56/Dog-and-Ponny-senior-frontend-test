<template>
  <div class="border-2 p-0 rounded mt-0">
    <div
      style="color: #34a6b9"
      v-on:click="isOpen = !isOpen"
      class="
        background-color:
        #34a6b9
        text-white
        py-1
        px-1
        font-bold
        rounded
        cursor-pointer
      "
    >
      {{ title }}
    </div>
    <div
      class="mt-4 border-2 p-2 rounded"
      :class="isOpen ? 'd-block' : 'hidden'"
    >
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      isOpen: false,
    };
  },
  name: "Accordion",
  props: {
    title: String,
  },
};
</script>