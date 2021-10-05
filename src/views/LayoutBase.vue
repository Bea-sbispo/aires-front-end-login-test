<template>
  <section class="container">
    <div class="container-background">
      <img src="../assets/background.png" alt="background" />
    </div>
    <div class="container-form">
      <slot />
    </div>
  </section>
</template>

<style lang="scss" scoped>
.container {
  min-height: 100vh;
  display: grid;
  grid-template-rows: 100vh;
  grid-template-columns: 2fr 1fr;
  grid-template-areas: 'background form';
}

.container-background {
  grid-area: background;
  position: relative;

  img {
    position: absolute;
    height: 100vh;
  }
}

.container-form {
  grid-area: form;
  background: #fff;
  z-index: 1;
  padding: 0 50px;
}

@media screen and (min-width: 1418px) {
  .container {
    grid-template-columns: auto 1fr;
  }

  .container-background {
    img {
      position: relative;
      height: 100vh;
    }
  }

  .container-form {
    padding: 0;
  }
}
</style>
