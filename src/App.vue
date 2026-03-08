<script setup>
import { ref } from "vue";

const usuarios = ref([]);

const nombre = ref("");
const email = ref("");
const pais = ref("");

function registrarUsuario() {
  const nuevoUsuario = {
    nombre: nombre.value,
    email: email.value,
    pais: pais.value,
  };

  usuarios.value.push(nuevoUsuario);

  nombre.value = "";
  email.value = "";
  pais.value = "";
}
</script>

<template>
  <header class="header">
    <h1>Registro de Usuarios</h1>
  </header>

  <main class="contenedor">
    <section class="form-section">
      <h2>Formulario</h2>

      <form @submit.prevent="registrarUsuario">
        <div class="campo">
          <label for="nombre">Nombre</label>

          <input
            id="nombre"
            type="text"
            v-model="nombre"
            required
            pattern="[A-Za-z ]{3,}"
            aria-label="Nombre del usuario"
            placeholder="Ingresa tu nombre"
          />
        </div>

        <div class="campo">
          <label for="email">Email</label>

          <input
            id="email"
            type="email"
            v-model="email"
            required
            aria-label="Correo electrónico"
            placeholder="correo@ejemplo.com"
          />
        </div>

        <div class="campo">
          <label for="pais">País</label>

          <select
            id="pais"
            v-model="pais"
            required
            aria-label="Seleccionar país"
          >
            <option value="">Selecciona un país</option>
            <option>Perú</option>
            <option>México</option>
            <option>España</option>
            <option>Chile</option>
          </select>
        </div>

        <button type="submit">Registrar</button>
      </form>
    </section>

    <section class="lista">
      <h2>Usuarios registrados</h2>

      <article class="usuario" v-for="(user, index) in usuarios" :key="index">
        <h3>{{ user.nombre }}</h3>
        <p>{{ user.email }}</p>
        <p>{{ user.pais }}</p>
      </article>
    </section>
  </main>
</template>

<style>
body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  background: #f4f6f8;
}

.header {
  background: #42b883;
  color: white;
  text-align: center;
  padding: 20px;
}

.contenedor {
  display: flex;
  gap: 40px;
  justify-content: center;
  padding: 40px;
  flex-wrap: wrap;
}

/* escritorio */
.form-section {
  background: white;
  padding: 25px;
  border-radius: 10px;
  width: 320px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.lista {
  width: 350px;
}

.campo {
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
}

input,
select {
  padding: 10px;
  border-radius: 6px;
  border: 1px solid #ccc;
  transition: 0.3s;
}

input:focus,
select:focus {
  border-color: #42b883;
  outline: none;
}

button {
  margin-top: 10px;
  padding: 12px;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  background: #369b72;
}

.usuario {
  background: white;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 8px;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
  transition: 0.3s;
}

.usuario:hover {
  transform: scale(1.02);
}

/* responsive celular */
@media (max-width: 700px) {
  .contenedor {
    flex-direction: column;
    align-items: center;
  }

  .form-section {
    width: 100%;
    max-width: 350px;
  }

  .lista {
    width: 100%;
    max-width: 350px;
  }
}
</style>
