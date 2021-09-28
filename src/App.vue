<template>
  <div id="app">
    <div class="grid">
      <div class="header">
        <BaseHeader username="Dr. Pablo Kehyaian" />
      </div>
      <div class="sidenav">
        <!-- placeholder -->
        <div class="sidenav-component"></div>
      </div>
      <main class="main">
        <ul class="breadcrumb">
          <li class="breadcrumb-item">Listado de Pacientes</li>
        </ul>

        <div class="container">
          <div class="d-f ai-c jc-sb">
            <!-- b -->
            <div class="title">
              <img
                class="title__icon"
                src="@/assets/icons/title-icon.svg"
                alt="main title icon"
              />
              <div class="title__text">
                <h1 class="title__text__main">Listado de Pacientes</h1>
                <p class="title__text__secondary">Visualización de pacientes</p>
              </div>
            </div>
            <!-- b -->

            <input class="search-input" placeholder="Buscar" type="text" />
          </div>

          <BaseButton text="Nuevo Paciente" />
          <BaseButton text="Descargar CSV" />

          <!-- {{pacientesArr}} -->

          <ul class="table">
            <li class="table-heading">
              <div class="table-cell">Nombre y Apellidos</div>
              <div class="table-cell">Clinica</div>
              <div class="table-cell">Objetivo Tratamiento</div>
              <div class="table-cell">Estado</div>
              <div class="table-cell">Acciones</div>
            </li>
            <li
              class="table-row"
              v-for="paciente in pacientesArr"
              :key="paciente.id"
            >
              <div class="table-cell table-row__name">
                <div>
                  <span>{{ paciente.datos_paciente.nombre }}</span>
                  <span>{{ paciente.datos_paciente.apellidos }}</span>
                </div>
              </div>
            </li>
          </ul>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import pacientes from "./data/pacientes.json";
import BaseHeader from "@/components/BaseHeader.vue";
import BaseButton from "@/components/BaseButton.vue";

export default {
  data() {
    return {
      pacientes,
    };
  },
  name: "App",
  components: {
    BaseHeader,
    BaseButton,
  },
  computed: {
    pacientesArr: function () {
      let res = [];
      const keys = Object.keys(this.pacientes);
      keys.forEach((key) => {
        res.push({ id: key, ...this.pacientes[key] });
      });
      return res;
    },
  },
};
</script>

<style lang="scss">
#app {
  // to fix: does not accept style import if empty
}

.button {
  cursor: pointer;
  background-color: $clr-white;
  border: 2px solid $clr-primary;
  border-radius: 5px;
  padding: 15px;

  display: flex;
  align-items: center;
  justify-content: center;
  color: $clr-primary;
  font-weight: bold;

  transition: all 0.25s ease-in-out;

  &:hover {
    background-color: $clr-primary;
    color: $clr-white;
  }

  img {
    margin-right: 15px;
    max-width: 15px;
    max-height: 15px;
    display: inline-block;
  }
}
</style>
