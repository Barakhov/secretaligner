<template>
  <div id="app">
    <div class="grid">
      <div class="header">
        <BaseHeader username="Dr. Pablo Kehyaian" />
      </div>
      <div class="sidenav">
        <div class="sidenav-component">
          <!-- placeholder -->
        </div>
      </div>
      <main class="main">
        <!-- start breadcrumb -->
        <ul class="breadcrumb">
          <li class="breadcrumb-item">Listado de Pacientes</li>
        </ul>
        <!-- end breadcrumb -->

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

            <BaseInput @dosearch="filterResults" />
          </div>

          <div class="d-f ai-c">
            <BaseButton class="primary" text="Nuevo Paciente" icon="plus" />
            <BaseButton class="primary" text="Descargar CSV" icon="file-download" />
          </div>

          <BaseTable :list="pacientesArrFiltered" />
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
import BaseInput from "@/components/BaseInput.vue";

export default {
  data() {
    return {
      pacientes,
      searchString: "",
    };
  },
  name: "App",
  components: {
    BaseHeader,
    BaseButton,
    BaseTable,
    BaseInput,
  },
  computed: {
    pacientesArr: function () {
      let res = [];
      const keys = Object.keys(this.pacientes);
      keys.forEach((key) => {
        this.pacientes[key].datos_paciente.iniciales =
          this.pacientes[key].datos_paciente.nombre.charAt(0).toUpperCase() +
          this.pacientes[key].datos_paciente.apellidos.charAt(0).toUpperCase();
        res.push({ id: key, ...this.pacientes[key] });
      });
      return res;
    },
    pacientesArrFiltered: function () {
      if (this.searchString === "") {
        return this.pacientesArr;
      } else {
        return this.pacientesArr.filter((el) => {
          return (
            (
              el.datos_paciente.nombre.toLowerCase() +
              " " +
              el.datos_paciente.apellidos.toLowerCase()
            ).indexOf(this.searchString) > -1
          );
        });
      }
    },
  },
  methods: {
    filterResults: function (searchstring) {
      this.searchString = searchstring.toLowerCase();
    },
  },
};
</script>

<style lang="scss">
.base-button:last-of-type {
  margin-left: 30px;
}
</style>
