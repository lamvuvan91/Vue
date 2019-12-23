
<template>
  <div>
    <h2>Board</h2>
    <Squares></Squares>
  </div>
</template>

<script>
import Squares from '@/components/Squares'
export default {
  name: 'Board',
  components:
  {
    Squares
  }
}
</script>
