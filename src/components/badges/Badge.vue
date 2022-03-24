<template>
  <div :class="{
    'text-success': isSuccessType,
    'text-primary': isPrimaryType,
    'text-info': isSecondaryType,
    'text-semibold': !isSuccessType
  }">
    <div class="flex items-center">
      <span class="icon" :class="{
        'icon-success': isSuccessType,
        'icon-calendar-check': isPrimaryType,
        'icon-calendar-empty opacity-20': isSecondaryType
      }"></span>

      <span class="capitalize ml-sm" :class="{'opacity-50': isSuccessType}">
        <slot />
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Badge',
  props: {
    type: {
      type: String,
      default: 'success'
    }
  },
  computed: {
    isSuccessType() {
      return this.type === 'success'
    },
    isPrimaryType() {
      return this.type === 'primary'
    },
    isSecondaryType() {
      return this.type === 'secondary'
    }
  }
}
</script>
