<template>
  <div class="main-footer">Copyright {{getTheYear()}}</div>
</template>

<script>
export default {
  name: "main-footer",
  data() {
    return {};
  },
  methods: {
    getTheYear: function() {
      return new Date().getFullYear();
    },
  },
  mounted() {
    getTheYear();
  },
};
</script>

<style>
</style>