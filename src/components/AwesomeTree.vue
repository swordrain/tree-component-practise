<script>
import AwesomeTreeNode from "./AwesomeTreeNode";
export default {
  name: "AwesomeTree", //递归调用必须指定name
  props: {
    nodes: {
      type: Array,
      default: function () {
        return [];
      },
    },
    level: {
      type: Number,
      default: 0,
    },
  },
  components: {
    AwesomeTreeNode,
  },
  render() {
    return (
      <div>
        {this.nodes.map((node) => {
          if (node.children && node.children.length > 0) {
            return (
              <ul>
                <awesome-tree-node key={node.key} node={node} level={this.level + 1} />
                <awesome-tree nodes={node.children} level={this.level + 1} />
              </ul>
            );
          } else {
            return (
              <ul>
                <awesome-tree-node key={node.key} node={node} level={this.level + 1} />
              </ul>
            );
          }
        })}
      </div>
    );
  },
};
</script>
<style scoped>
ul {
  list-style-type: none;
  margin-block-start: 0;
  margin-block-end: 0;
  margin-inline-start: 0;
  margin-inline-end: 0;
  padding-inline-start: 0;
}
</style>
