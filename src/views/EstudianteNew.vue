<template>
  <div class="row mt-5">
    <div class="col-md-6 offset-md-3">
      <div class="card shadow-lg border-0 rounded-3">
        <div class="card-header bg-primary text-white text-center fs-5 fw-bold">
          <i class="bi bi-person-plus-fill me-2"></i>
          Registrar Estudiante
        </div>
        <div class="card-body p-4">
          <form>
            <div class="text-center mb-3">
              <img
                v-if="foto"
                :src="foto"
                alt="foto"
                id="fotoimg"
                class="img-thumbnail rounded-circle shadow-sm"
                style="width: 100px; height: 100px; object-fit: cover;"
              />
              <img
                v-else
                src="https://cdn4.iconfinder.com/data/icons/small-n-flat/24/user-64.png"
                alt="foto"
                id="fotoimg"
                class="img-thumbnail rounded-circle shadow-sm"
                style="width: 100px; height: 100px; object-fit: cover;"
              />
            </div>

            <!-- Ejemplo de campos -->
            <div class="mb-3">
              <label class="form-label fw-semibold">Nombre</label>
              <input type="text" id="nombre" class="form-control" placeholder="Ingrese nombre" />
            </div>
            <div class="mb-3">
              <label class="form-label fw-semibold">Apellido</label>
              <input type="text" id="apellido" class="form-control" placeholder="Ingrese apellido" />
            </div>

            <div class="mb-3">
              <label class="form-label fw-semibold">Imagen</label>
              <input v-on:change="previsualizarFoto" type="file" accept="image/png, image/jpeg, image/gif" class="form-control" placeholder="Ingrese correo" />
            </div>

            <div class="d-grid">
              <button type="submit" class="btn btn-success">
                <i class="bi bi-save me-2"></i> Guardar
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { mostrarAlerta , confirmar } from "../funciones";

export default {
  data() {
    return {
      nombre:'',
      apellido:'',
      foto:'',
      url:'http://academico-backend.test/api/v1/estudiantes',
      cargando:false
     
    };
  },
    methods: {
    guardar() {
      this.cargando = true;

      
      
    },
    previsualizarFoto(event){
        var reader = new FileReader();
        reader.readAsDataURL(event.target.files[0]);
        reader.onload = function(){
            var miFoto = document.getElementById('fotoimg');
            miFoto.src = reader.result;
            this.foto =  miFoto.src;
        
        }
    }
  }
  
}
</script>
