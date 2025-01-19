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
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px 50px;
}

.container-background {
  display: none;
}

.container-form,
.form-container {
  width:100%;
  background: #fff;
}

@media screen and (min-width: 910px) {
  .container {
    height: 100vh;
    display: grid;
    padding: 0;
    grid-template-columns: repeat(2, 1fr);
  }

  .container-background {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    img {
      height: 100%;
      width: 100%;

    }
  }

  .container-form {
    padding: 0 30px;
  }
}

</style>
