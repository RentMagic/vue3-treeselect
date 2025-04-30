<script>
  import { onLeftClick } from '../utils'
  import DeleteIcon from './icons/Delete'

  export default {
    name: 'vue-treeselect--multi-value-item',
    inject: [ 'instance' ],

    props: {
      node: {
        type: Object,
        required: true,
      },
    },

    methods: {
      handleMouseDown: onLeftClick(function handleMouseDown() {
        const { instance, node } = this

        // Deselect this node.
        instance.select(node)
      }),
    },

    render() {
      const { instance, node } = this
      const colorClass = node.Color ? `bg-[#${node.Color}]` : ''
      const itemClass = {
        [colorClass]: !!colorClass,
      }

      console.log(itemClass);
      
      const customValueLabelRenderer = instance.$slots['value-label']
      const labelRenderer = customValueLabelRenderer ? customValueLabelRenderer({ node }) : node.label

      return (
        <div class="">
          <div class={itemClass} onMousedown={this.handleMouseDown}>
            <span class="vue-treeselect__multi-value-label">{ labelRenderer }</span>
            <span class="vue-treeselect__icon vue-treeselect__value-remove"><DeleteIcon /></span>
          </div>
        </div>
      )
    },
  }
</script>
