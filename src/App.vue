<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@100;300;400;700;900&display=swap');
*,
*::after,
*::before {
    margin: 0;
    padding: 0;
    box-sizing: inherit;
}

html {
    // This defines what 1rem should be
    font-size: 62.5%;
}

body {
    font-family: "Lato", sans-serif;
    font-weight: 400;
    line-height: 1.7;
    color: $color-gray;
    padding: 3rem;
    box-sizing: border-box;
}

</style>
