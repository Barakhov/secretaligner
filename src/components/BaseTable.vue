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
      <li>5</li>
      <li>10</li>
      <li>15</li>
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
      <li class="table-row" v-for="item in list" :key="item.id">
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
          <div class="base-button">
            Acciones
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  username: "BaseTable",
  data() {
    return {
      viewMode: "table",
    };
  },
  props: {
    list: [],
  },
  methods: {
    toggleViewMode(view) {
      this.viewMode = view;
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
    justify-content: space-between;

    .table-row {
      flex: 0 1 100%;
      border-top: 1px solid $clr-light-grey;
      margin-bottom: 30px;
      box-shadow: 0px 3px 7px -5px $clr-dark-grey;
      background-color: $clr-ultra-light-grey;

      @media (min-width: 580px) {
        flex: 0 1 48%;
      }
      @media (min-width: 768px) {
        flex: 0 1 32%;
      }
      @media (min-width: 1024px) {
        flex: 0 1 24%;
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
</style>
