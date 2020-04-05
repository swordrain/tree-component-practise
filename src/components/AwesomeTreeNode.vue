<template>
  <li>
    <div
      class="indicator"
      @click="$emit('toggle', node.key)"
      :class="computeIndicatorClass"
      :style="{
        display: 'inline-block',
        height: indicatorWidth + 'px',
        width: indicatorWidth + 'px',
      }"
    />
    {{ node.label }}
  </li>
</template>

<script>
const OFFSET = 18;
const INDICATOR_WIDTH = 18;
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
    isFirst: {
      type: Boolean,
      default: false,
    },
    isLast: {
      type: Boolean,
      default: false,
    },
    isLeaf: {
      type: Boolean,
      default: true,
    },
    isExpand: {
      type: Boolean,
      default: false,
    },
    toggle: {
      type: Function,
    },
  },
  data: function () {
    return {
      offset: OFFSET,
      indicatorWidth: INDICATOR_WIDTH,
    };
  },
  computed: {
    computeIndicatorClass: function () {
      if (this.isFirst && this.isLast && this.isExpand && !this.isLeaf) {
        return "unique-expand";
      }
      if (this.isFirst && this.isLast && !this.isExpand && !this.isLeaf) {
        return "unique-collapse";
      }
      if (this.isFirst && this.isExpand && !this.isLeaf) {
        return "first-expand";
      }
      if (this.isFirst && !this.isExpand && !this.isLeaf) {
        return "first-collapse";
      }
      if (this.isLast && this.isExpand && !this.isLeaf) {
        return "last-expand";
      }
      if (this.isLast && !this.isExpand && !this.isLeaf) {
        return "last-collapse";
      }
      if (!this.isFirst && !this.isLast && this.isExpand && !this.isLeaf) {
        return "middle-expand";
      }
      if (!this.isFirst && !this.isLast && !this.isExpand && !this.isLeaf) {
        return "middle-collapse";
      }
      if (this.isFirst && this.isLast && this.isLeaf) {
        return "unique-leaf";
      }
      if (this.isFirst && this.isLeaf) {
        return "first-leaf";
      }
      if (this.isLast && this.isLeaf) {
        return "last-leaf";
      }
      if (!this.isFirst && !this.isLast && this.isLeaf) {
        return "middle-leaf";
      }
      return "";
    },
  },
};
</script>
<style>
.indicator {
  background-image: url("/zTreeStandard.png");
  background-repeat: no-repeat;
  background-position: center center;
}
.indicator:hover {
  cursor: pointer;
  opacity: 0.8;
}
.unique-expand {
  background-position: -92px -54px;
}
.unique-collapse {
  background-position: -74px -54px;
}
.first-expand {
  background-position: -92px 0;
}
.first-collapse {
  background-position: -74px 0;
}
.last-expand {
  background-position: -92px -36px;
}
.last-collapse {
  background-position: -74px -36px;
}
.middle-expand {
  background-position: -92px -18px;
}
.middle-collapse {
  background-position: -74px -18px;
}
.first-leaf {
  background-position: -56px -18px;
}
.last-leaf {
  background-position: -56px -36px;
}
.middle-leaf {
  background-position: -56px -18px;
}
</style>
