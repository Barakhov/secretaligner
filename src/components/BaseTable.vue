<template>
  <ul class="table">
    <li class="table-heading">
      <div class="table-cell">Nombre y Apellidos</div>
      <div class="table-cell">Clinica</div>
      <div class="table-cell">Objetivo Tratamiento</div>
      <div class="table-cell">Estado</div>
      <div class="table-cell">Acciones</div>
    </li>
    <li class="table-row" v-for="item in list" :key="item.id">
      <div class="table-cell table-row__name">
        <div>
          {{ item.datos_item.nombre.charAt(index) }}
          {{ item.datos_item.apellidos.charAt(index) }}
        </div>
        <div>
          <span>{{ item.datos_item.nombre }}</span>
          <span>{{ item.datos_item.apellidos }}</span>
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  username: "BaseTable",
  props: {
    list: [],
  },
};
</script>

<style lang="scss" scoped></style>
