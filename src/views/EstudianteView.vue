<template>
  <div class="row mt-5">
    <div class="col-md-6 offset-md-3">
      <div class="card shadow-lg border-0 rounded-3">
        <div class="card-header bg-primary text-white text-center fs-5 fw-bold">
          <i class="bi bi-person-plus-fill me-2"></i>
          Detalle Estudiante
        </div>
        <div class="card-body p-4">
          <router-link :to="{path:'/'}" class="btn btn-info">

            <i class="fa-solid fa-arrow-left"></i>Regresar a la lista
          </router-link>
        
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
              <label type="text" id="nombre" v-text="nombre" class="form-control" placeholder="Ingrese nombre"></label> 
            </div>
            <div class="mb-3">
              <label class="form-label fw-semibold">Apellido</label>
              <label type="text" id="apellido" v-text="apellido" class="form-control" placeholder="Ingrese apellido" ></label>
            </div>

            
      
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { mostrarAlerta , enviarSolicitud } from "../funciones";
import { useRoute } from "vue-router";

export default {
  data() {
    return {
      id:0,
      nombre:'',
      apellido:'',
      foto:'',
      url:'http://academico-backend.test/api/v1/estudiantes',
      cargando:false
     
    };
  },
  mounted(){
    const route = useRoute();
    this.id = route.params.id;
    this.url += '/'+this.id;
    this.getEstudiante();

  },
    methods: {
    getEstudiante(){
      axios.get(this.url).then(
        res => {
          this.nombre = res.data.data.nombre;
          this.apellido = res.data.data.apellido;
          this.foto = res.data.data.foto;
        }
      );

    },
    actualizar() {
         event.preventDefault();
        var miFoto = document.getElementById('fotoimg');
       
        this.foto = miFoto.src;
        if(this.nombre.trim()===''){
            mostrarAlerta('Ingrese un nombre','warning','nombre');
        }
        else if(this.apellido.trim()===''){
            mostrarAlerta('Ingrese un apellido','warning','apellido');
        }
        else{
            var parametros = {nombre:this.nombre.trim(),apellido:this.apellido.trim(),foto:this.foto.trim(),}
            enviarSolicitud('PUT',parametros,this.url,'Estudiante Actualizado')

        }


      
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
