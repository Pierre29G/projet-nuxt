<template>

<div>
  <label>{{name}} :</label>
    <input :type="type" :name="name">
</div>

</template>

<script>
  export default {
    props:{
      type: String,
      name: String
    }
    }
</script>