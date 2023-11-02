<template>
  <div :class="currentTheme">
    <router-view></router-view>
  </div>
</template>
<script>
import { computed } from 'vue';
import { useStore } from 'vuex';
export default {
  setup() {
    const store = useStore();
    const currentTheme = computed(() => store.state.theme);
    return {
      currentTheme,
    };
  },
};
</script>