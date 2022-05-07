<template>
  <input
    type="text"
    class="search-bar"
    :value="query"
    placeholder="search..."
  />
</template>

<script>
export default {
props:['query']
};
</script>

<style>
</style>