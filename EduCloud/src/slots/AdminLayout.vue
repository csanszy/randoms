<script setup>

</script>

<template>
  <div class="flex h-[100dvh] w-[100dvw] bg-creamy_white">

    <div class="w-[22dvw] border-r">
      <slot name="left"/>
    </div>

    <div class="w-[78dvw]">
      <slot name="right"/>
    </div>
  </div>

</template>