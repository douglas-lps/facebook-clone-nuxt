<template>
  <form @submit.prevent="onSubmit">
    <div class="fom-field">
      <BaseInput
        v-model="user.email"
        type="email"
        placeholder="E-mail"
        readonly
      />
    </div>
    <div class="fom-field">
      <BaseInput v-model="user.name" type="text" placeholder="Nome" />
    </div>
    <div class="fom-field">
      <BaseInput v-model="user.password" type="password" placeholder="Senha" />
    </div>
    <div class="fom-field">
      <BaseInput
        v-model="user.passwordConfirmation"
        type="password"
        placeholder="Repita a senha"
      />
    </div>
    <BaseButton text="Próxima etapa" />
  </form>
</template>

<script lang="ts">
import Vue from 'vue'
import { userRegister } from '@/store'

export default Vue.extend({
  data() {
    return {
      user: {
        email: userRegister.$user.email,
        name: '',
        password: '',
        passwordConfirmation: ''
      }
    }
  },
  methods: {
    async onSubmit() {
      try {
        await userRegister.update({
          key: this.$route.params.key,
          ...this.user
        })

        alert(
          'Cadastro realizado com sucesso, agora você já pode efetuar seu login.'
        )

        this.user.email = ''
        this.user.name = ''
        this.user.password = ''
        this.user.passwordConfirmation = ''
      } catch (error) {
        alert('Erro ao tentar efetuar cadastro.')
      }
    }
  }
})
</script>
<style lang="scss" scoped>
form {
  display: grid;
  grid-gap: 0.8rem;
  button {
    width: 100%;
  }
  a {
    justify-self: end;
    font-size: 14px;
    color: color(white);
  }
  input {
    width: 100% !important;
    padding: 0.7rem 1.2rem;
  }
}
</style>
