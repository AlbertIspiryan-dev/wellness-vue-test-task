<template>
  <div class="flex items-center radius-md border list-iem">
    <div>
      {{ itemData.title }}
    </div>

    <div class="flex items-center ml-auto minw-xl">
      <badge :type="badgeType">
        {{ statusLabel }}
      </badge>

      <div class="ml-auto">
        <button class="relative btn-link" @click="toogleDropdown">
          <span class="icon icon-options opacity-20"></span>

          <div class="dropdown" v-show="activeItem === itemData.id">
            <ul>
              <li class="py-md text-error text-semibold" @click.stop="deleteItem">Delete</li>
            </ul>
          </div>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Badge from '@/components/badges/Badge.vue'

export default {
  name: 'ListItem',
  components: {
    Badge,
  },
  props: {
    itemData: {
      type: Object,
      required: true
    }
  },
  computed: {
    statusLabel() {
      if (this.itemData.status === 'pending') {
        return 'book now'
      }

      return this.itemData.status
    },
    badgeType() {
      switch (this.itemData.status) {
        case 'booked':
          return 'primary'
        case 'pending':
          return 'secondary'
        default: 
          return 'success'
      }
    }
  },
  data() {
    return {
      activeItem: -1
    }
  },
  methods: {
    toogleDropdown() {
      if (this.activeItem !== -1) {
        this.activeItem = -1
        return
      }

      this.activeItem = this.itemData.id
    },
    deleteItem() {
      this.$emit('deleteItem', this.itemData.id)
      this.toogleDropdown()
    }
  }
}
</script>