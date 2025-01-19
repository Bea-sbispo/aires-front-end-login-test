<template>
  <layout-base>
    <div class="form-container">
      <img class="logo" src="../assets/img/logo.svg" alt="Logo" />
      <h2>Crie sua conta</h2>
      <small>Crie a sua conta Aires.</small>

      <form @submit.prevent="submit">
        <div class="form-group">
          <label for="email">E-mail</label>
          <input
            id="email"
            placeholder="E-mail"
            type="email"
            v-model="user.email"
            class="form-control"
          />
        </div>
        <div class="form-group">
          <label for="password">Senha</label>
          <input
            id="password"
            placeholder="Senha"
            type="password"
            v-model="user.password"
            class="form-control"
            :class="{ error: hasError && !checkEqualPassword }"
          />
        </div>
        <div class="form-group">
          <label for="password">Confirme sua senha</label>
          <input
            id="confirm_password"
            placeholder="Senha"
            type="password"
            v-model="user.confirm_password"
            class="form-control"
            :class="{ error: hasError && !checkEqualPassword }"
          />
        </div>
        <button class="button-create" type="submit">Criar conta</button>
      </form>

      <div class="forgot-container">
        <span>Já possui uma conta?</span>
        <router-link class="link" :to="{ name: 'Login' }">
          Clique para acessar
        </router-link>
      </div>
      <router-link class="forgot-password link" :to="{ name: 'Cadastro' }">
        Esqueceu sua senha?
      </router-link>
    </div>
  </layout-base>
</template>

<script>
import LayoutBase from './LayoutBase.vue';

export default {
  components: {
    LayoutBase,
  },
  data: () => ({
    user: {
      email: null,
      password: null,
      confirm_password: null,
    },
    hasError: false,
  }),
  computed: {
    checkEqualPassword() {
      return this.user.password === this.user.confirm_password;
    },
  },
  methods: {
    submit() {
      // Validar
      this.hasError = false;
      // Checar dados
      if (!this.checkEqualPassword) {
        this.hasError = true;
        return;
      }

      // Proxima pagina
      localStorage.setItem('user', JSON.stringify(this.user));
      this.$router.push({ name: 'Login' });
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../styles/variables';

.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: max-content;
  height: 100%;
  margin: auto;
  font-size: 1.4rem;
  animation: appearFromRight 700ms;

  .logo {
    width: 100px;
    height: 100px;
  }

  .link {
    font-size: 1.4rem;
    color: $primary;
    text-decoration: none;
    transition: 500ms;

    &:hover {
      text-decoration: underline;
    }
  }
  .forgot-password {
    margin-top: 30px;
  }

  h2 {
    margin-top: 50px;
    font-size: 4rem;
    letter-spacing: 2.8px;
  }

  small {
    margin-top: 30px;
    font-weight: 300;
    font-size: 1.6rem;
    letter-spacing: 1px;
    color: $gray;
  }

  form {
    width: 100%;
    margin-top: 30px;

    .form-group {
      margin-bottom: 3%;

      & ~ .form-group {
        margin-top: 30px;
      }

      label {
        font-weight: 500;
        font-size: 1.4rem;
        color: $black;
      }

      .form-control {
        width: 100%;
        height: 46px;
        background: #ffffff 0% 0% no-repeat padding-box;
        box-shadow: 0px 0px 12px #00000029;
        border-radius: 10px;
        padding: 10px;
        margin-top: 10px;
        border: none;

        &::placeholder {
          font-size: 1.3rem;
          color: $gray;
        }

        &.error {
          border: red solid 2px;
        }
      }
    }

    .button-create {
      width: 100%;
      min-height: 17px;
      font-weight: normal;
      font-size: 1.8rem;
      text-align: center;
      color: #fff;
      margin-top: 30px;
      padding: 10px 0;
      border-radius: 10px;
      border: none;
      background: linear-gradient(to right, $primary, $primary-dark);
    }
  }
}

.forgot-container {
  margin-top: 63px;

  span {
    margin-right: 15px;
  }
}

@keyframes appearFromRight {
  from {
    opacity: 0;
    transform: translateX(100px);
  }

  to {
    opacity: 1;
    transform: translateX(0);
  }
}
</style>
