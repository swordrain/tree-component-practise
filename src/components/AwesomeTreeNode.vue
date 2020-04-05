<template>
  <li>
    <div :style="{ display: 'inline-block', width: offset * (level - 1) + 'px' }"></div>
    {{ node.label }}
  </li>
</template>

<script>
const OFFSET = 20;
export default {
  props: {
    node: {
      type: Object,
      default: function () {
        return {};
      },
    },
    level: {
      type: Number,
      default: 0,
    },
  },
  data: function () {
    return {
      offset: OFFSET,
    };
  },
};
</script>
