<template>
  <div>
    <b-table striped hover :items="markers"></b-table>
  </div>
</template>

<script>
export default {
  props: {
    markers: Object
  }
}
</script>
