<template>
  <section class="bg-red-500">
    <h2>Registro de Usuarios</h2>
    <form @submit.prevent="registerUser" class="bg-[#123456]">
        <div>
            <label>Correo Electrónico</label>
            <input type="email" id="email" v-model="email" placeholder="Introduce tu email" required>
        </div>
        <div>
            <label>Contraseña</label>
            <input type="password" id="password" v-model="password" placeholder="Introduce una contraseña" required>
        </div>
        <button type="submit">Registrarse</button>
        <p>Ya tienes cuenta <router-link to="/login">Iniciar sesión</router-link></p>
    </form>
  </section>
</template>

<script>
import { auth } from "@/db/firebase"
import { createUserWithEmailAndPassword } from "firebase/auth"
export default {
    name:'RegisterView',
    data(){
        return{
            email: "",
            password: ""
        }
    },
    methods:{
        async registerUser(){
            try {
                await createUserWithEmailAndPassword(auth, this.email, this.password)
                this.$router.push('/perfil')
            } catch (error) {
                console.error("Error al registrar usuario: ", error.message)
                alert(error.message)
            }
        }
    }
}
</script>