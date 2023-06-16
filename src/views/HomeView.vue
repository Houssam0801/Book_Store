<template>
  <div class="home">
    <PageContent />
  </div>
</template>

<script>
// @ is an alias to /src

import PageContent from "@/components/PageContent.vue";

export default {
  name: "HomeView",
  data() {
    return {};
  },
  methods: {},

  components: {
    PageContent,
  },
};
</script>
