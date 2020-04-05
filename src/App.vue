<template>
  <div id="app">
    <awesome-tree :nodes="nodes" />
  </div>
</template>

<script>
import AwesomeTree from "./components/AwesomeTree.vue";
export default {
  name: "App",
  data: function () {
    return {
      nodes: [
        {
          label: "Node1",
          expand: true,
          key: "1",
          children: [
            {
              label: "Node1-1",
              key: "1-1",
            },
            {
              label: "Node1-2",
              key: "1-2",
            },
            {
              label: "Node1-3",
              key: "1-3",
              children: [
                {
                  label: "Node1-3-1",
                  key: "1-3-1",
                },
                {
                  label: "Node1-3-2",
                  key: "1-3-2",
                },
              ],
            }
          ],
        },
        {
          label: "Node2",
          key: "2",
        },
        {
          label: "Node3",
          expand: false,
          key: "3",
          children: [
            {
              label: "Node3-1",
              key: "3-1",
            },
            {
              label: "Node3-2",
              key: "3-2",
            },
            {
              label: "Node3-3",
              key: "3-3",
            },
          ],
        },
      ],
    };
  },
  components: {
    AwesomeTree,
  },
};
</script>

<style></style>
