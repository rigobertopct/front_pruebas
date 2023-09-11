<template>
  <div class="mt-4 row">
    <div class="col-12">
      <div class="card shadow-lg">
        <!-- Card header -->
        <div class="card-header">
          <h5 class="mb-0">Disciplina</h5>
        </div>
        <div class="d-flex justify-content-between m-3">
          <div class="col-3">
            <div class="input-group">
              <input v-model="name" type="text" class="form-control border-bottom border-dark input-icon"
                     placeholder="Buscar" aria-label="Recipient's username" aria-describedby="button-addon2">
            </div>
          </div>
          <div class="col-8 text-end">
            <button @click="openModal" class="btn btn-dark align-content-end">
              <i class="fa fa-plus-square me-2"></i> Nuevo
            </button>
          </div>
          <div class="col-1"></div>
        </div>
        <div class="table-responsive">
          <table id="datatable-basic" class="table table-flush">
            <thead class="thead-light">
            <tr>
              <th
                class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7"
              >
                Nombre
              </th>
              <th
                class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7"
              >
                Deporte
              </th>
              <th
                class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7"
              >
                Acciones
              </th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="item in disciplinaPorNombre" :key="item.id">
              <td class="text-sm font-weight-normal ps-4">{{ item.nombre }}</td>
              <td class="text-sm font-weight-normal ps-4">{{ item.deporte.nombre }}</td>
              <td class="text-sm font-weight-normal ps-4">
                <div class="btn-group" role="group">
                  <!--                  <button v-if="deporte.isActive" data-bs-toggle="tooltip"-->
                  <!--                          data-bs-placement="top" title="Desactivar Marca" data-container="body"-->
                  <!--                          data-animation="true" class="btn btn-warning p-1 ms-1">-->
                  <!--                    <i class="material-icons opacity-10">block</i></button>-->
                  <!--                  <button v-else data-bs-toggle="tooltip" data-bs-placement="top"-->
                  <!--                          title="Activar Marca" data-container="body" data-animation="true"-->
                  <!--                          class="btn btn-success p-1 ms-1">-->
                  <!--                    <i class="material-icons opacity-10">check_circle</i></button>-->
                  <button @click="openUpdate(item.id, item.nombre, item.deporte.id)"
                          data-bs-toggle="tooltip"
                          data-bs-placement="top"
                          title="Editar Marca" data-container="body" data-animation="true"
                          class="btn btn-info p-1 ms-1">
                    <i class="material-icons opacity-10">edit</i></button>
                  <button data-bs-toggle="tooltip" data-bs-placement="top"
                          title="Eliminar Marca" data-container="body" data-animation="true"
                          class="btn btn-danger p-1 ms-1">
                    <i class="material-icons opacity-10">delete</i></button>
                </div>
              </td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
    <div class="divModal Nuevo">
      <div v-if="showModal" :class="['modal', { 'show': showModal }]" @transitionend="onTransitionEnd">
        <div class="modal-content">
          <div class="row mb-3 border-bottom border-dark">
            <h4 class="text-start"><i class="fa fa-plus-square me-2"></i>Nuevo Deporte<i @click="closeModal"
                                                                                         class="material-icons-round opacity-10 modal-icon">close</i>
            </h4>
          </div>
          <div class="row mb-3">
            <div class="col-12">
              <label class="form-label">Nombre</label>
              <input v-model="nombre" class="form-control border-bottom border-dark p-2"
                     placeholder="Escriba el nombre de una Aseguradora" type="text">
              <label class="form-label">Deporte</label>
              <select v-model="deporte" class="form-control border-bottom border-dark p-2">
                <option value="0" disabled>Seleccione un Deporte</option>
                <option v-for="elemento in allDeportes" :key="elemento.id" :value="elemento.id">{{ elemento.nombre }}
                </option>
              </select>
              <div v-show="error" class="text-danger mt-3 text-center p-2"
                   style="background-color: rgba(255,19,28,0.08)">
                <div class="d-flex align-center justify-content-center"><i class="material-icons-round opacity-10 me-2">error</i>
                  <p class="text-dark">No pueden haber campos vacíos</p></div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-6 d-flex justify-content-start">
              <button @click="closeModal" class="btn btn-secondary" type="button">Cancelar</button>
            </div>
            <div class="col-6 d-flex justify-content-end">
              <button @click="Guardar" class="btn btn-dark" type="button">Guardar</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="divModal Actualizar">
      <div v-if="showUpdate" :class="['modal', { 'show': showUpdate }]" @transitionend="onTransitionEnd">
        <div class="modal-content">
          <div class="row mb-3 border-bottom border-dark">
            <h4 class="text-start"><i class="fa fa-pencil-square me-2"></i>Actualizar Deporte<i @click="closeUpdate"
                                                                                                class="material-icons-round opacity-10 modal-icon">close</i>
            </h4>
          </div>
          <div class="row mb-3">
            <div class="col-12">
              <label class="form-label">Nombre</label>
              <input v-model="nombre" class="form-control border-bottom border-dark p-2"
                     placeholder="Escriba el nombre de una Aseguradora" type="text">
              <label class="form-label">Deporte</label>
              <select v-model="deporte" class="form-control border-bottom border-dark p-2">
                <option value="0" disabled>Seleccione un Deporte</option>
                <option v-for="elemento in allDeportes" :key="elemento.id" :value="elemento.id">{{ elemento.nombre }}
                </option>
              </select>
              <div v-show="error" class="text-danger mt-3 text-center p-2"
                   style="background-color: rgba(255,19,28,0.08)">
                <div class="d-flex align-center justify-content-center"><i class="material-icons-round opacity-10 me-2">error</i>
                  <p class="text-dark">No pueden haber campos vacíos</p></div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-6 d-flex justify-content-start">
              <button @click="closeUpdate" class="btn btn-secondary" type="button">Cancelar</button>
            </div>
            <div class="col-6 d-flex justify-content-end">
              <button @click="Actualizar" class="btn btn-dark" type="button">Guardar</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import gql from "graphql-tag";
import Swal from "sweetalert2";

const SELECT = gql`{
  allDeportes{
        id
        nombre
        isActivo
  }
}
`;
const BUSCAR = gql`query DisciplinaPorNombre($name:String!) {
    disciplinaPorNombre(name: $name) {
         id
        nombre
        isActivo
        deporte {
            id
            nombre
            isActivo
        }
    }
}`;
const NUEVO = gql`mutation NuevaDisciplina($nombre:String!, $deporte:Int!) {
    nuevaDisciplina(nombre: $nombre, deporte:$deporte) {
        success
        error
    }
}`;
const ACTUALIZAR = gql`mutation ActualizarDisciplina($id:Int!, $nombre:String!, $deporte:Int!) {
    actualizarDisciplina(id: $id, nombre: $nombre, deporte:$deporte) {
        success
        error
    }
}`;
export default {
  name: "Disciplina",
  data() {
    return {
      disciplinaPorNombre: [],
      allDeportes: [],
      name: "",
      showModal: false,
      error: false,
      deporte: 0,
      nombre: "",
      id: 0,
      showUpdate: false
    };
  },
  apollo: {
    disciplinaPorNombre: {
      query: BUSCAR,
      variables() {
        return {
          name: this.name
        };
      },
      fetchPolicy: "cache-and-network"
    },
    allDeportes: {
      query: SELECT,
      fetchPolicy: "cache-and-network"
    }
  },
  methods: {
    async Guardar() {
      if (this.nombre === "") {
        this.error = true;
        return false;
      }
      await this.$apollo.mutate({
        mutation: NUEVO,
        variables: {
          nombre: this.nombre,
          deporte: this.deporte
        },
        refetchQueries: [{ query: BUSCAR, variables: { name: this.name } }]
      }).then(response => {
        if (response.data.nuevaDisciplina.success) {
          const Toast = Swal.mixin({
            toast: true,
            position: "top-end",
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
            didOpen: (toast) => {
              toast.addEventListener("mouseenter", Swal.stopTimer);
              toast.addEventListener("mouseleave", Swal.resumeTimer);
            }
          });
          Toast.fire({
            icon: "success",
            title: "Creado correctamente"
          });
        } else {
          const Toast = Swal.mixin({
            toast: true,
            position: "top-end",
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
            didOpen: (toast) => {
              toast.addEventListener("mouseenter", Swal.stopTimer);
              toast.addEventListener("mouseleave", Swal.resumeTimer);
            }
          });
          Toast.fire({
            icon: "error",
            title: response.data.nuevaDisciplina.error
          });
        }
        this.closeModal();
      }).catch(error => {
        const Toast = Swal.mixin({
          toast: true,
          position: "top-end",
          showConfirmButton: false,
          timer: 3000,
          timerProgressBar: true,
          didOpen: (toast) => {
            toast.addEventListener("mouseenter", Swal.stopTimer);
            toast.addEventListener("mouseleave", Swal.resumeTimer);
          }
        });
        Toast.fire({
          icon: "error",
          title: error
        });
        this.closeModal();
      });
    },
    async Actualizar() {
      if (this.nombre === "" || this.deporte === 0) {
        this.error = true;
        return false;
      }
      await this.$apollo.mutate({
        mutation: ACTUALIZAR,
        variables: {
          deporte: this.deporte,
          nombre: this.nombre,
          id: this.id
        },
        refetchQueries: [{ query: BUSCAR, variables: { name: this.name } }]
      }).then(response => {
        if (response.data.actualizarDisciplina.success) {
          const Toast = Swal.mixin({
            toast: true,
            position: "top-end",
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
            didOpen: (toast) => {
              toast.addEventListener("mouseenter", Swal.stopTimer);
              toast.addEventListener("mouseleave", Swal.resumeTimer);
            }
          });
          Toast.fire({
            icon: "success",
            title: "Actualizado correctamente"
          });
        } else {
          const Toast = Swal.mixin({
            toast: true,
            position: "top-end",
            showConfirmButton: false,
            timer: 3000,
            timerProgressBar: true,
            didOpen: (toast) => {
              toast.addEventListener("mouseenter", Swal.stopTimer);
              toast.addEventListener("mouseleave", Swal.resumeTimer);
            }
          });
          Toast.fire({
            icon: "error",
            title: response.data.actualizarDisciplina.error
          });
        }
        this.closeUpdate();
      }).catch(error => {
        const Toast = Swal.mixin({
          toast: true,
          position: "top-end",
          showConfirmButton: false,
          timer: 3000,
          timerProgressBar: true,
          didOpen: (toast) => {
            toast.addEventListener("mouseenter", Swal.stopTimer);
            toast.addEventListener("mouseleave", Swal.resumeTimer);
          }
        });
        Toast.fire({
          icon: "error",
          title: error
        });
        this.closeUpdate();
      });
    },
    openModal() {
      this.showModal = true;
      this.error = false;
      document.body.classList.add("modal-open");
    },
    openUpdate(id, nombre, deporte) {
      this.id = id;
      this.nombre = nombre;
      this.deporte = deporte;
      this.showUpdate = true;
      this.error = false;
      document.body.classList.add("modal-open");
    },
    closeModal() {
      this.nombre = "";
      this.deporte = 0;
      this.showModal = false;
      this.error = false;
      document.body.classList.remove("modal-open");
    },
    closeUpdate() {
      this.nombre = "";
      this.id = 0;
      this.deporte = 0;
      this.showUpdate = false;
      this.error = false;
      document.body.classList.remove("modal-open");
    },
    onTransitionEnd(event) {
      if (event.propertyName === "opacity" && !this.showModal) {
        this.$emit("close");
      }
    }
  }
};
</script>

<style scoped>
.input-icon {
  background-image: url('../../assets/img/icons/search.png');
  background-repeat: no-repeat;
  background-position: 10px center;
  background-size: 20px;
  padding-left: 38px; /* ajusta el padding para que el texto no se solape con el icono */
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 9999;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-icon {
  position: absolute;
  top: 10px;
  right: 10px;
  cursor: pointer;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 15px;
  width: 50%;
}

.modal {
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
}

.modal.show {
  opacity: 1;
}
</style>
