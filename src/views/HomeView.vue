<template>
  <div class="row">
    <div class="col-12 col-lg-10 offset-lg-1">
      <div class="table-responsive">
        <table class="table table-sm table-bordered table-hover align-middle text-center">
          <thead class="table-dark">
            <tr>
              <th scope="col">#</th>
              <th scope="col">ID</th>
              <th scope="col">FOTO</th>
              <th scope="col">NOMBRE</th>
              <th scope="col">APELLIDO</th>
              <th scope="col">REGISTRO</th>
              <th scope="col">ACCIONES</th>
            </tr>
          </thead>
          <tbody id="contenido">
            <tr v-if="cargando">
              <td colspan="7" class="text-center">
                <h5>Cargando...</h5>
              </td>
            </tr>
            <tr v-else v-for="(est, i) in estudiantes" :key="est.id">
              <td>{{ i + 1 }}</td>
              <td>{{ est.id }}</td>
              <td>
                <img
                  v-if="est.foto"
                  :src="est.foto"
                  alt="foto"
                  class="img-thumbnail"
                  style="max-width: 60px !important;" 
                />
                <img
                  v-else="est.foto"
                  height="30"
                  src="https://cdn4.iconfinder.com/data/icons/small-n-flat/24/user-64.png"
                  alt="foto"
                  class="img-thumbnail"
                />

              </td>
              <td class="text-truncate" style="max-width:120px">{{ est.nombre }}</td>
              <td class="text-truncate" style="max-width:120px">{{ est.apellido }}</td>
              <td>{{ new Date(est.created_at).toLocaleDateString('es-ES') }}</td>
              <td>
                <router-link :to="{ path: 'view/' + est.id }" class="btn btn-info btn-sm me-1">
                  <i class="fa-solid fa-eye"></i>
                </router-link>
                &nbsp;
                <router-link :to="{ path: 'edit/' + est.id }" class="btn btn-warning btn-sm">
                  <i class="fa-solid fa-edit"></i>
                </router-link>
                 &nbsp;
                <button :to="{ path: 'edit/' + est.id }" class="btn btn-danger btn-sm">
                  <i class="fa-solid fa-trash"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      estudiantes: null,
      cargando: false,
    };
  },
  mounted() {
    this.getEstudiantes();
  },
  methods: {
    getEstudiantes() {
      this.cargando = true;
      axios.get("http://academico-backend.test/api/v1/estudiantes").then((res) => {
        this.estudiantes = res.data;
        this.cargando = false;
      });
    },
  },
};
</script>
