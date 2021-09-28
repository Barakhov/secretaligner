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
            <!-- start title -->
            <div class="title">
              <i class="far fa-address-card title__icon"></i>
              <div class="title__text">
                <h1 class="title__text__main">Listado de Pacientes</h1>
                <p class="title__text__secondary">Visualización de pacientes</p>
              </div>
            </div>
            <!-- end title -->
            <input class="search-input" placeholder="Buscar" type="text" />
          </div>

          <div class="d-f ai-c">
            <BaseButton text="Nuevo Paciente" icon="plus" />
            <BaseButton text="Descargar CSV" icon="file-download" />
          </div>

          <BaseTable :list="pacientesArr" />
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import pacientes from "./data/pacientes.json";
import BaseHeader from "@/components/BaseHeader.vue";
import BaseButton from "@/components/BaseButton.vue";
import BaseTable from "@/components/BaseTable.vue";

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
    BaseTable,
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
</style>
