<template>
  <div class="about">
    <h1>About Page</h1>
    <p>{{ asd }}</p>
    <p>{{ test }}</p>
  </div>
</template>

<script>
export default {
  name: "About",
  data() {
    return {
      asd: process.env.NODE_ENV,
      test: process.env.BASE_URL
    };
  }
};
</script>
