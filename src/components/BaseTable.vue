<template>
  <ul class="table">
    <li class="table-row table-row--heading">
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
      <div class="table-cell">
        <div class="d-f">
          <div class="table-cell__icon d-f ai-c jc-c">
            <span>{{
              item.datos_paciente.nombre.charAt(0).toUpperCase()
            }}</span>
            <span>{{
              item.datos_paciente.apellidos.charAt(0).toUpperCase()
            }}</span>
          </div>
          <div>
            <p>
              {{ item.datos_paciente.nombre }}
              {{ item.datos_paciente.apellidos }}
            </p>
            <p class="table-cell__date">
              <i class="far fa-calendar-alt"></i>
              {{ item.datos_paciente.fecha_nacimiento }}
            </p>
          </div>
        </div>
      </div>
      <div class="table-cell">
        {{ item.ficha_dental.clinica }}
      </div>
      <div class="table-cell">
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
      <div class="table-cell">ACCIONES</div>
    </li>
  </ul>
</template>

<script>
export default {
  username: "BaseTable",
  props: {
    list: [],
  },
  // methods: {
  //   firstCharUpper(string) {
  //     return string.charAt(0).toUpperCase();
  //   },
  // },
};
</script>

<style lang="scss" scoped>
.table {
  display: flex;
  flex-flow: column nowrap;
  background-color: $clr-white;
  width: 100%;
  margin: 0 auto;
  padding: 0;
}

.table-row {
  display: flex;
  flex-flow: row nowrap;
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
    background-color: #71e7b9;
  }
  &:nth-child(3n - 2) .table-cell__icon {
    background-color: #ebe66e;
  }
  &:nth-child(3n) .table-cell__icon {
    background-color: #6cbbe8;
  }
}

.table-cell {
  display: flex;
  flex: 1;
  font-size: 14px;
  padding: 10px 0;
  justify-content: center;
  align-items: center;

  &:first-child {
    justify-content: flex-start;
  }

  &__icon {
    min-width: 35px;
    height: 35px;
    margin: 0 7px 0 10px;
    border-radius: 100%;
  }

  &__date {
    font-size: 14px;
    color: $clr-mid-grey;
  }
}

// .table-row:last-child {
//   border-bottom: 0;
// }

.state {
  padding: 10px;
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
