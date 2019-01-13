<template>
  <div class="home">
    <wedding />
  </div>
</template>

<script>
// @ is an alias to /src
import Wedding from '@/components/Wedding.vue'

export default {
  name: 'home',
  components: {
    wedding: Wedding
  }
}
</script>
