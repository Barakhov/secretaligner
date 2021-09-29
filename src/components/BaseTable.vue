<template>
  <div>
    <ul class="table-controls d-f ai-c">
      <li
        :class="viewMode === 'table' ? 'selected' : ''"
        @click="toggleViewMode('table')"
      >
        <i class="fas fa-bars"></i>
      </li>
      <li
        :class="viewMode === 'cards' ? 'selected' : ''"
        @click="toggleViewMode('cards')"
      >
        <i class="fas fa-th-large"></i>
      </li>
      <li
        @click="setItemsPerPage(item.items)"
        :class="item.selected ? 'selected' : ''"
        v-for="item in itemsPerPageArr"
        :key="item.items"
      >
        {{ item.items }}
      </li>
    </ul>
    <ul
      class="table"
      :class="viewMode === 'table' ? 'table--table-view' : 'table--cards-view'"
    >
      <li v-if="viewMode === 'table'" class="table-row table-row--heading">
        <div class="table-cell">
          Nombre y Apellidos
          <i class="fas fa-sort"></i>
        </div>
        <div class="table-cell">
          Clinica
          <i class="fas fa-sort"></i>
        </div>
        <div class="table-cell">
          Objetivo Tratamiento
          <i class="fas fa-sort"></i>
        </div>
        <div class="table-cell">
          Estado
          <i class="fas fa-sort"></i>
        </div>
        <div class="table-cell">
          Acciones
          <i class="fas fa-sort"></i>
        </div>
      </li>
      <li
        class="table-row"
        v-for="item in list.slice(sliceStart, sliceEnd)"
        :key="item.id"
      >
        <div class="table-cell table-cell--name">
          <div class="d-f">
            <div
              v-if="viewMode === 'table'"
              class="table-cell__icon d-f ai-c jc-c"
            >
              <span>{{ item.datos_paciente.iniciales }}</span>
            </div>
            <div>
              <p>
                {{ item.datos_paciente.nombre }}
                {{ item.datos_paciente.apellidos }}
              </p>
              <p class="table-cell--date">
                <i class="far fa-calendar-alt"></i>
                {{ item.datos_paciente.fecha_nacimiento }}
              </p>
            </div>
          </div>
        </div>
        <div class="table-cell table-cell--clinic">
          <i
            v-if="viewMode === 'cards'"
            class="table-cell__card-icon fas fa-clinic-medical"
          ></i>
          <span>{{ item.ficha_dental.clinica }}</span>
        </div>
        <div class="table-cell table-cell--objective">
          <i
            v-if="viewMode === 'cards'"
            class="table-cell__card-icon fas fa-notes-medical"
          ></i>
          {{ item.ficha_dental.objetivo_tratamiento }}
        </div>
        <div class="table-cell">
          <div class="state" :class="`state--${item.ficha_dental.estado}`">
            {{
              item.ficha_dental.estado.charAt(0).toUpperCase() +
              item.ficha_dental.estado.slice(1)
            }}
          </div>
        </div>
        <div class="table-cell">
          <BaseDropdown
            :optionList="['Editar', 'Finalizar', 'Borrar']"
            v-show="viewMode === 'table'"
            text="Acciones"
          />

          <div v-show="viewMode === 'cards'" class="w100 mt20 d-f ai-c jc-sa">
            <BaseButton small text="Editar" />
            <BaseButton small text="Finalizar" />
            <BaseButton small text="Borrar" />
          </div>
        </div>
      </li>
    </ul>

    <!-- <p>
      {{ currentPage }}
      of
      {{ totalPages }}
    </p> -->

    <div class="d-f ai-c jc-c">
      <ul class="table-pagination d-f ai-c jc-se">
        <li
          v-for="page in totalPages"
          :key="page"
          :class="currentPage === page ? 'selected' : ''"
          class="table-pagination__item"
        >
          <span @click="setPage(page)">{{ page }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import BaseDropdown from "@/components/BaseDropdown.vue";
import BaseButton from "@/components/BaseButton.vue";

export default {
  username: "BaseTable",
  components: {
    BaseDropdown,
    BaseButton,
  },
  data() {
    return {
      viewMode: "table",
      currentPage: 1,
      itemsPerPageArr: [
        {
          items: 5,
          selected: false,
        },
        {
          items: 10,
          selected: true,
        },
        {
          items: 15,
          selected: false,
        },
      ],
    };
  },
  props: {
    list: [],
  },
  methods: {
    toggleViewMode(view) {
      this.viewMode = view;
    },
    setItemsPerPage(item) {
      this.itemsPerPageArr.filter((el) => el.selected)[0].selected = false;
      this.itemsPerPageArr.filter((el) => el.items === item)[0].selected = true;
      this.currentPage = 1;
    },
    setPage(page) {
      this.currentPage = page;
    },
  },
  computed: {
    itemsPerPage: function () {
      return this.itemsPerPageArr.filter((el) => el.selected)[0].items;
    },
    totalItems: function () {
      return this.list.length;
    },
    totalPages: function () {
      return Math.ceil(this.totalItems / this.itemsPerPage);
    },
    sliceStart: function () {
      return (this.currentPage - 1) * this.itemsPerPage;
    },
    sliceEnd: function () {
      return (this.currentPage - 1) * this.itemsPerPage + this.itemsPerPage;
    },
  },
};
</script>

<style lang="scss" scoped>
.table {
  display: flex;
  background-color: $clr-white;
  width: 100%;
  margin: 0 auto;
  padding: 0;

  &--table-view {
    flex-flow: column nowrap;

    .table-row {
      display: flex;
      flex-flow: row nowrap;
    }
  }

  &--cards-view {
    display: flex;
    flex-wrap: wrap;
    // justify-content: space-between;

    .table-row {
      flex: 0 1 100%;
      padding: 5px;
      margin: 0 1% 20px 1%;
      border-top: 1px solid $clr-light-grey;
      box-shadow: 0px 3px 7px -5px $clr-dark-grey;
      background-color: $clr-ultra-light-grey;

      @media (min-width: 580px) {
        flex: 0 1 48%;
      }
      @media (min-width: 768px) {
        flex: 0 1 31%;
      }
      @media (min-width: 1024px) {
        flex: 0 1 23%;
      }
    }

    .table-cell--name {
      justify-content: center;
      font-size: 16px;
      font-weight: 700;
      margin-top: 10px;
      text-align: center;
    }

    .table-cell--date {
      text-align: center;
      margin: 10px 0 15px;
    }

    .table-cell--clinic,
    .table-cell--objective {
      padding: 5px 0;
      color: $clr-dark-grey;
    }
  }
}

.table-row {
  width: 100%;
  border-bottom: 1px solid $clr-light-grey;
  border-right: 1px solid $clr-light-grey;
  border-left: 1px solid $clr-light-grey;

  &--heading {
    border-right: none;
    border-left: none;
    cursor: pointer;

    i {
      margin-left: 5px;
      color: $clr-mid-grey;
    }
  }

  &:nth-child(3n - 1) .table-cell__icon {
    background-color: $clr-initials-1;
  }
  &:nth-child(3n - 2) .table-cell__icon {
    background-color: $clr-initials-2;
  }
  &:nth-child(3n) .table-cell__icon {
    background-color: $clr-initials-3;
  }
}

.table-cell {
  display: flex;
  flex: 1;
  font-size: 14px;
  padding: 10px 0;
  justify-content: center;
  align-items: center;

  &--name {
    justify-content: flex-start;
  }

  &--date {
    font-size: 14px;
    color: $clr-mid-grey;
  }

  &__icon {
    min-width: 35px;
    height: 35px;
    margin: 0 7px 0 10px;
    border-radius: 100%;
    color: $clr-white;
  }

  &__card-icon {
    margin-right: 5px;
    transform: translateY(-2px);
  }
}

.table-controls {
  padding: 0;
  margin-top: 25px;
  margin-bottom: 25px;

  li {
    cursor: pointer;
    font-size: 18px;
    font-weight: 700;
    margin: 0 8px 0 0;
    padding: 0 4px;
    min-width: 20px;
    text-align: center;
    transition: all 0.15s ease-in-out;
    border-radius: 2px;

    &:hover,
    &.selected {
      background-color: $clr-primary;
      color: $clr-white;
    }
  }
}

.state {
  padding: 8px 18px;
  border-radius: 20px;
  color: $clr-white;

  &--enviado {
    background-color: $clr-enviado;
  }
  &--facturado {
    background-color: $clr-facturado;
  }
  &--fabricando {
    background-color: $clr-fabricando;
  }
  &--planificando {
    background-color: $clr-planificando;
  }
  &--aceptado {
    background-color: $clr-aceptado;
  }
  &--solicitado {
    background-color: $clr-solicitado;
  }
}

.table-pagination {
  padding: 0;

  &__item {
    width: 50px;
    height: 50px;
    cursor: pointer;
    text-align: center;
    line-height: 50px;
    border-top: 1px solid $clr-mid-grey;
    border-bottom: 1px solid $clr-mid-grey;

    &:first-child {
      border-left: 1px solid $clr-mid-grey;
      border-top-left-radius: 10px;
      border-bottom-left-radius: 10px;
    }
    &:last-child {
      border-right: 1px solid $clr-mid-grey;
      border-top-right-radius: 10px;
      border-bottom-right-radius: 10px;
    }

    &.selected {
      background-color: $clr-primary;
      color: $clr-white;
    }

    span {
      display: block;
      width: 100%;
      height: 100%;
    }
  }
}
</style>
