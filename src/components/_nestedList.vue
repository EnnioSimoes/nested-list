<template>
  <ul class="pl-5 border" :class="{'bg-red-600': draggingBg}" @dragover.prevent @dragenter.prevent>
    <li
      v-for="item in list"
      :key="item.order"
      :draggable="true"
      @dragstart="emitStartDrag($event, item)"
      @drag="$emit('dragging')"
    >
      <nodeMenu :title="item.title" :link="item.link" @input-update="alert(event[0])" />
      <nestedList v-if="item.children" :list="item.children" @startDrag="emitStartDrag($event[0], $event[1])" @dragging="$emit('dragging')" />
    </li>
  </ul>
</template>

<script setup>
import nodeMenu from './_nodeMenu.vue'
import nestedList from './_nestedList.vue'
import { ref, defineProps, defineEmits } from 'vue'

// const props =
defineProps({
  list: {
    type: Array,
    default: () => [],
  },
})

const emit = defineEmits(['startDrag', 'dragging'])

const draggingBg = ref(false)
const buttonkey = ref(0)
const startDragCount = ref(0)

const emitStartDrag = (event, item) => {
  if (startDragCount.value === 0) {
    console.log('emitStartDrag')
    emit('startDrag', [event, item])
    // console.log('#event:', event)
    // console.log('#item:', item)
    draggingBg.value = true
    buttonkey.value = ++buttonkey.value
    startDragCount.value = startDragCount.value + 1
  } else {
    startDragCount.value = startDragCount.value = 0
  }
}

// const numerarItens = (item, id) => {
//   return item.level = id
// }

// Classificar niveis do menu e add o grupo nas ul
// const itensRecursive = (links, itemId = 0) => {
//   links.forEach(element => {
//     // if (ref > 0) {
//     //   itemId = ref + '.' + itemId
//     // }
//     numerarItens(element, itemId)
//     itemId = itemId + 1
//     if (element.children) {
//       itensRecursive(element.children)
//     }
//     console.log(element.title, ' = ', element.level)
//   })
//   return links
// }


// const res = itensRecursive(props.list)
// console.log('res', res)

// const startDrag = (evt, item) => {
//   console.log('startDrag')
//   console.log('evt', evt)
//   console.log('item', item)
//   console.log('titulo: ', evt.originalTarget.innerText)
//   evt.dataTransfer.dropEffect = 'move'
//   evt.dataTransfer.effectAllowed = 'move'
//   // evt.dataTransfer.setData('itemID', item.id)
// }

// const dragging = () => {
//   draggingBg.value = true
//   console.log('dragging')
// }

// const onDragover = (group) => {
//   console.log('onDragover: ', group)
// }

// const onDrop = (evt) => {
//   draggingBg.value = false
//   console.log('onDrop')
//   console.log('evt', evt)
//   // console.log('linksMenu', linksMenu.value)
//   console.log('titulo: ', evt.originalTarget.innerText)
//   // const itemID = evt.dataTransfer.getData('itemID')
//   // console.log('itemID', itemID)
//   // const item = linksMenu.find((item) => item.id == itemID)
//   // item.list = list
// }
</script>
