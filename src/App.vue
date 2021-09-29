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
          <li class="breadcrumb-item">{{ pageTitle }}</li>
        </ul>
        <!-- end breadcrumb -->

        <div class="container">
          <div class="d-f ai-c jc-sb">
            <BaseTitle>
              {{ pageTitle }}
              <template v-slot:secondary> Visualización de pacientes </template>
            </BaseTitle>
            <BaseSearch @dosearch="filterResults" />
          </div>

          <div class="d-f ai-c">
            <BaseButton
              @click="showModal"
              class="primary"
              text="Nuevo Paciente"
              icon="plus"
            />
            <download-csv :data="pacientesArrCSV">
              <BaseButton
                class="primary"
                text="Descargar CSV"
                icon="file-download"
              />
            </download-csv>
          </div>
          <BaseTable :list="pacientesArrFiltered" />
        </div>
      </main>
    </div>
    <BaseModal v-show="isModalVisible" @close="closeModal">
      <h2 class="ta-c mb20">Añadir Nuevo Paciente</h2>
      <form>
        <fieldset class="d-f">
          <input type="text" placeholder="Nombre" />
          <input type="text" placeholder="Apellidos" />
        </fieldset>

        <fieldset class="d-f">
          <input type="date" />
          <select name="sexo">
            <option disabled selected>Selecciona una opción</option>
            <option value="m">Masculino</option>
            <option value="f">Femenino</option>
          </select>
        </fieldset>

        <fieldset class="d-f">
          <textarea rows="3" placeholder="Clínica"></textarea>
        </fieldset>

        <fieldset class="d-f jc-fs ai-c mb10">
          <input type="checkbox" id="cb1" /><label for="cb1"
            >Recorte Alineadores</label
          >
        </fieldset>
        <fieldset class="d-f jc-fs ai-c mb10">
          <input type="checkbox" id="cb2" /><label for="cb2"
            >¿SecretRetainer?</label
          >
        </fieldset>
        <div class="w100 bt-separator mb20 px5 d-f ai-c jc-sb">
          <BaseButton small text="Guardar" />
          <BaseButton small text="Cancelar" />
          <BaseButton small text="Limpiar" />
        </div>
      </form>
    </BaseModal>
  </div>
</template>

<script>
import pacientes from "./data/pacientes.json";
import BaseHeader from "@/components/BaseHeader.vue";
import BaseButton from "@/components/BaseButton.vue";
import BaseTable from "@/components/BaseTable.vue";
import BaseSearch from "@/components/BaseSearch.vue";
import BaseModal from "@/components/BaseModal.vue";
import BaseTitle from "@/components/BaseTitle.vue";

export default {
  data() {
    return {
      pacientes,
      searchString: "",
      isModalVisible: false,
      pageTitle: "Listado de Pacientes",
    };
  },
  name: "App",
  components: {
    BaseHeader,
    BaseButton,
    BaseTable,
    BaseSearch,
    BaseModal,
    BaseTitle,
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
    pacientesArrCSV: function () {
      return this.pacientesArrFiltered.map((el) => {
        return {
          Nombre: el.datos_paciente.nombre,
          Apellidos: el.datos_paciente.apellidos,
          Clinica: el.ficha_dental.clinica,
          "Objetivo tratamiento": el.ficha_dental.objetivo_tratamiento,
          Estado: el.ficha_dental.estado,
        };
      });
    },
  },
  methods: {
    filterResults: function (searchstring) {
      this.searchString = searchstring.toLowerCase();
    },
    showModal: function () {
      this.isModalVisible = true;
    },
    closeModal: function () {
      this.isModalVisible = false;
    },
  },
};
</script>

<style lang="scss">
@import "@/assets/styles/scss/components/_forms.scss";

.base-button.primary:first-child {
  margin-right: 30px;
}
</style>
