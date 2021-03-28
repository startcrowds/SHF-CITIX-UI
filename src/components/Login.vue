<template>
    <div class="login">
        <form @submit.prevent="login">
            <h3>Ingresa a tu Tienda</h3>

            <div class="form-group">
                <label>Correo Electrónico</label>
                <input v-model="email" type="email" class="form-control form-control-lg" />
            </div>

            <div class="form-group">
                <label>Contraseña</label>
                <input v-model="password" type="password" class="form-control form-control-lg" />
            </div>
			<p v-if="error" class="error">Correo Electrónico o Contraseña Equivocada</p>
            <button type="submit" class="btn btn-dark btn-lg btn-block">Ingresar</button>

            <p class="forgot-password text-right mt-2 mb-4">
                <router-link to="/forgot-password">Olvidó su Contraseña?</router-link>
            </p>

            <div class="social-icons">
                <ul>
                    <li><a href="#"><i class="fa fa-google"></i></a></li>
                    <li><a href="#"><i class="fa fa-facebook"></i></a></li>
                    <li><a href="#"><i class="fa fa-twitter"></i></a></li>
                </ul>
            </div>

        </form>
    </div>
</template>

<script>
import auth from "@/logic/auth";
export default {
  data: () => ({
    email: "",
    password: "",
    error: false
  }),
  methods: {
    async login() {
      try {
        await auth.login(this.email, this.password);
        this.$router.push("/tiendas-list");
      } catch (error) {
        this.error = true;
      }
    }
  }
};
</script>