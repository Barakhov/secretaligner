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

            <BaseSearch @dosearch="filterResults" />
          </div>

          <div class="d-f ai-c">
            <BaseButton
              @click="showModal"
              class="primary"
              text="Nuevo Paciente"
              icon="plus"
            />
            <BaseButton
              class="primary"
              text="Descargar CSV"
              icon="file-download"
            />
          </div>

          <BaseTable :list="pacientesArrFiltered" />
        </div>
      </main>
    </div>
    <BaseModal v-show="isModalVisible" @close="closeModal">
      <form>

          <fieldset class="d-f">
            <input type="text" placeholder="Nombre" />
            <input type="text" placeholder="Apellidos" />
          </fieldset>


          <fieldset class="d-f">
            <input type="date" />
            <select name="sexo">
              <option value="m">Masculino</option>
              <option value="f">Femenino</option>
            </select>
          </fieldset>

          <fieldset class="d-f">
            <textarea name="" id="" cols="30" rows="3"></textarea>
          </fieldset>

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

export default {
  data() {
    return {
      pacientes,
      searchString: "",
      isModalVisible: false,
    };
  },
  name: "App",
  components: {
    BaseHeader,
    BaseButton,
    BaseTable,
    BaseSearch,
    BaseModal,
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
