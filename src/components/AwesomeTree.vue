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
    isParentLastNode: {
      type: Boolean,
      default: false,
    },
  },
  data: function () {
    return {
      cache: {},
    };
  },
  components: {
    AwesomeTreeNode,
  },
  methods: {
    onToggle: function (key) {
      if (this.cache[key].expand === undefined) {
        this.$set(this.cache[key], "expand", true);
      } else {
        this.cache[key].expand = !this.cache[key].expand;
      }
    },
  },
  render() {
    return (
      <ul class={!this.isParentLastNode && this.level ? "line-conn tree" : "tree"}>
        {this.nodes.map((node, index) => {
          if (node.children && node.children.length > 0) {
            this.cache[node.key] = node;
            return (
              <ul>
                <awesome-tree-node
                  key={node.key}
                  node={node}
                  level={this.level + 1}
                  isFirst={index === 0}
                  isLast={index === this.nodes.length - 1}
                  isExpand={node.expand}
                  isLeaf={!node.children || node.children.length === 0}
                  vOn:toggle={this.onToggle}
                />
                {node.expand && (
                  <awesome-tree
                    nodes={node.children}
                    level={this.level + 1}
                    isParentLastNode={index === this.nodes.length - 1}
                  />
                )}
              </ul>
            );
          } else {
            return (
              <awesome-tree-node
                key={node.key}
                node={node}
                level={this.level + 1}
                isFirst={index === 0}
                isLast={index === this.nodes.length - 1}
                isExpand={node.expand}
                isLeaf={!node.children || node.children.length === 0}
                vOn:toggle={this.onToggle}
              />
            );
          }
        })}
      </ul>
    );
  },
};
</script>
<style scoped>
.tree,
.tree ul,
.tree li {
  list-style-type: none;
  font-size: 12px;
  margin-block-start: 0;
  margin-block-end: 0;
  margin-inline-start: 0;
  margin-inline-end: 0;
  padding-inline-start: 0;
  display: block;
  max-height: 1000px;
  overflow: hidden;
}
.tree > li {
  padding-left: 18px;
}
.tree > ul {
  padding-left: 18px;
}
.tree li {
  display: flex;
}
.line-conn {
  background-image: url(/line_conn.gif);
  background-repeat: repeat-y;
}
</style>
