<template>
  <layout-base>
    <div class="form-container">
      <img class="logo" src="../assets/logo.svg" alt="Logo" />
      <h2>Acesso via e-mail</h2>
      <small>Acesse sua conta Aires por algum método abaixo</small>

      <form @submit.prevent="submit">
        <div class="form-group">
          <label for="email">E-mail</label>
          <input
            id="email"
            placeholder="E-mail"
            type="email"
            v-model="user.email"
            class="form-control"
            :class="{ error: hasError }"
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
            :class="{ error: hasError }"
          />
        </div>
        <div class="form-group">
          <div class="keep-conect">
            <input type="checkbox" name="continue" id="continue" />
            <label for="continue">
              Continuar conectado
            </label>
            <a class="link" href="/cadastro">Esqueceu sua senha?</a>
          </div>
        </div>
        <button class="button-submit" type="submit">Acessar</button>
      </form>

      <div class="forgot-container">
        <span>Não possui uma conta?</span>
        <router-link class="link" :to="{ name: 'Cadastro' }">
          Clique para criar a sua conta
        </router-link>
      </div>
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
    },
    hasError: false,
  }),
  methods: {
    submit() {
      // Validar
      this.hasError = false;
      const userStorage = JSON.parse(localStorage.getItem('user'));
      if (!userStorage) {
        this.$router.push({ name: 'Cadastro' });
        return;
      }
      // Checar dados
      const checkEmail = this.user.email === userStorage.email;
      const checkPassword = this.user.password === userStorage.password;

      if (!checkEmail || !checkPassword) {
        this.hasError = true;
        alert('Usuário não econtrado.');
        return;
      }

      // Proxima pagina
      alert('LOGOU');
    },
  },
  mounted() {
    setTimeout(() => {
      localStorage.removeItem('user');
    }, 20000);
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

    .button-submit {
      width: 100%;
      min-height: 17px;
      font-weight: normal;
      font-size: 1.8rem;
      text-align: center;
      color: #fff;
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

.keep-conect {
  display: flex;
  align-items: center;

  input {
    width: 26px;
    height: 26px;
  }

  label {
    margin-left: 15px;
  }
  a {
    margin-left: 70px;
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
