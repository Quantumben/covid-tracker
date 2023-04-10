<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">
      {{ title }}
    </h2>
    <div class="text-2xl mt-4 mb-10">
      {{ dataDate }}
    </div>
  </div>
</template>

<script>
export default {
  name: "DataTitle",
  props: ["title", "dataDate"],
};
</script>
