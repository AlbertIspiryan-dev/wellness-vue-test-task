<template>
  <div class="card border radius-md">
    <div class="flex items-center justify-between">
      <slot name="title" />

      <span class="inline-block relative cursor-pointer text-medium text-gray hide" @click="isOpen = !isOpen">hide</span>
    </div>


    <collapse-transition>
      <div v-show="isOpen">
        <slot />
      </div>
    </collapse-transition>
  </div>
</template>

<script>
import { CollapseTransition } from '@ivanv/vue-collapse-transition'

export default {
  name: 'Card',
  components: {
    CollapseTransition
  },
  props: {
    collapsable: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      isOpen: true
    }
  }
}
</script>
