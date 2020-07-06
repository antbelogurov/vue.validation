<template>
  <div class="container mt-4 text-center">
    <form>
      <h1>Введите данные</h1>
      <div class="form-group">
        <input
          placeholder="Email"
          type="email"
          id="email"
          class="form-control"
          v-model="email"
          :class="{'is-invalid':$v.email.$error}"
          @blur="$v.email.$touch()"
        />
        <div class="invalid-feedback" v-if="!$v.email.required">Данное поле обязательно к заполнению</div>
        <div class="invalid-feedback" v-if="!$v.email.email">Не является Email</div>
      </div>

      <div class="form-group">
        <input
          placeholder="Password"
          type="password"
          id="password"
          class="form-control"
          v-model="password"
          :class="{'is-invalid':$v.password.$error}"
          @blur="$v.password.$touch()"
        />
        <div
          class="invalid-feedback"
          v-if="!$v.password.minLength"
        >Минимальная длинна пароля {{$v.password.$params.minLength.min}} символов. На данный момент {{password.length}}.</div>
      </div>

      <div class="form-group">
        <input
          placeholder="Confirm password"
          type="password"
          id="confPass"
          class="form-control"
          :class="{'is-invalid':$v.confPass.$error}"
          @blur="$v.confPass.$touch()"
          v-model="confPass"
        />
        <div class="invalid-feedback" v-if="!$v.confPass.sameAs">Пароли не совпадают.</div>
      </div>

      <button class="btn btn-success btn-lg">Log In</button>
    </form>
  </div>
</template>

<script>
import { required, email, minLength, sameAs } from "vuelidate/lib/validators";

export default {
  data() {
    return {
      email: "",
      password: "",
      confPass: ""
    };
  },
  validations: {
    email: {
      required,
      email
    },
    password: {
      minLength: minLength(6)
    },
    confPass: {
      sameAs: sameAs("password")
    }
  }
};
</script>

<style scoped>
.container {
  margin: auto;
  width: 100%;
  max-width: 400px;
}
button {
  width: 100%;
}
</style>
