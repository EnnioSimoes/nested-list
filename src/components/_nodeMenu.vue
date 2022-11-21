<template>
  <div>
    <div class="bg-gray-100 hover:bg-gray-300 cursor-move p-2 rounded-md text-gray-800 text-sm shadow-md m-1 flex relative">
      <div v-if="editNode" class="absolute bg-white  p-2 rounded shadow-md -top-16 flex w-full">
        <div class="w-full">
          <input type="text" class="h-6 form-input" :value="title" />
          <input type="text" class="h-6 mt-1 form-input" :value="link" />
        </div>
        <div>
          <button class="align-baseline mx-2 bg-green-600 p-1 rounded text-white" title="Ok" @click.prevent="$emit('inputUpdate', [title, link])">
            <Icons icon="check" class="h-4" />
          </button>
          <button class="align-baseline mx-2 bg-red-600 p-1 rounded text-white mt-1" title="Cancelar" @click.prevent="editNode = false">
            <Icons icon="cancel" class="h-4" />
          </button>
        </div>
      </div>
      <span class="cursor-pointer" @click.prevent="editNode = !edit">{{ title }}</span>
      <!-- <button>
        <Icons class="w-4 mx-1" icon="pencil-square" />
      </button> -->
      <button>
        <Icons class="w-4 mx-1" icon="chevron-up" />
      </button>
      <button>
        <Icons class="w-4 mx-1" icon="chevron-down" />
      </button>
      <button>
        <Icons class="w-4 mx-1" icon="plus" />
      </button>
    </div>
  </div>
</template>

<script setup>
import Icons from './Icons.vue'
import { ref, defineProps, defineEmits } from 'vue'

defineEmits({
  inputUpdate: Array,
})

defineProps({
  title: {
    type: String,
    default: 'Empty',
  },
  link: {
    type: String,
    default: 'Empty',
  },
  edit: {
    type: Boolean,
    default: false,
  },
})

const editNode = ref(false)
</script>
