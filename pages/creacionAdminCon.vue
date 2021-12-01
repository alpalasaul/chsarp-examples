<template>
  <v-card>
    <v-responsive :aspect-ratio="16 / 9">
      <h1 style="text-align: center; margin-bottom: 10px">
        Ingreso de Administradores y Controladores
      </h1>
      <img class="imagen" src="/administradores.svg" />
      <div class="container">
        <v-row>
          <v-col cols="12">
            <v-chip class="ma-2" color="#6398E4" outlined>
              <v-icon left> mdi-account-cog </v-icon>
              Elija el tipo de usuario que desea ingresar:
              <v-switch
                style="margin-left: 6px; padding-bottom: 15px"
                v-model="sadmin"
                color="#CCD5E2"
                value="secondary"
                label="Administrador"
                hide-details
              ></v-switch>
              <v-switch
                style="margin-left: 6px; padding-bottom: 15px"
                v-model="scon"
                color="#CCD5E2"
                value="secondary"
                label="Controlador"
                hide-details
              ></v-switch>
            </v-chip>
          </v-col>
        </v-row>

        <v-row align="center" justify="center">
          <v-col cols="12" sm="15" md="8" v-if="sadmin">
            <v-card-text class="elevation-12" id="card-in">
              <v-form ref="form" lazy-validation v-model="valid">
                <p>Por favor ingrese los datos del nuevo administrador:</p>
                <v-text-field
                  ref="nombres"
                  label="Nombres"
                  outlined
                  rounded
                  v-model="nombres"
                  :rules="[() => !!nombres || 'Campo obligatorio']"
                  type="text"
                  color="primary"
                >
                </v-text-field>
                <v-text-field
                  ref="apellidos"
                  label="Apellidos"
                  outlined
                  rounded
                  v-model="apellidos"
                  :rules="[rules.required]"
                  type="text"
                  color="primary"
                >
                </v-text-field>
                <v-text-field
                  ref="cedula"
                  label="Cédula"
                  outlined
                  rounded
                  v-model="cedula"
                  :rules="[rules.cedula, rules.counter, rules.required, rules.ced]"
                  counter
                  maxlength="10"
                  color="primary"
                >
                </v-text-field>

               <v-text-field
                  v-model="fechaNacimiento"
                  label="Fecha de Nacimiento"
                  outlined
                  rounded
                  type="date"
                  name="user_date"
                  id="user_date"
                
                ></v-text-field>
                <v-text-field
                  ref="telefono"
                  label="Teléfono"
                  outlined
                  rounded
                  v-model="telefono"
                  :rules="[rules.tel, rules.counter, rules.required]"
                  counter
                  maxlength="10"
                  color="primary"
                >
                </v-text-field>
                <v-select
                  :items="generos"
                  label="Género"
                  outlined
                  rounded
                  v-model="genero"
                  :rules="[() => !!genero || 'Campo obligatorio']"
                ></v-select>
                <v-text-field
                  ref="correo"
                  label="Correo electrónico"
                  outlined
                  rounded
                  v-model="correo"
                  type="email"
                  :rules="[rules.email, rules.required]"
                  color="primary"
                >
                </v-text-field>
              </v-form>
            </v-card-text>

            <v-btn
              id="btn-ingreso"
              color="secondary"
              :disabled="!valid"
             @click="calculateAge"
            >
              Agregar
            </v-btn>
          </v-col>
        </v-row>

        <v-row align="center" justify="center">
          <v-col cols="12" sm="15" md="8" v-if="scon">
            <v-card-text class="elevation-12" id="card-in">
              <v-form ref="form" lazy-validation v-model="valid">
                <p>Por favor ingrese los datos del nuevo controlador:</p>
                <v-text-field
                  ref="nombres"
                  label="Nombres"
                  outlined
                  rounded
                  v-model="nombres"
                  :rules="[() => !!nombres || 'Campo obligatorio']"
                  type="text"
                  color="primary"
                >
                </v-text-field>
                <v-text-field
                  ref="apellidos"
                  label="Apellidos"
                  outlined
                  rounded
                  v-model="apellidos"
                  :rules="[rules.required]"
                  type="text"
                  color="primary"
                >
                </v-text-field>
                <v-text-field
                  ref="cedula"
                  label="Cédula"
                  outlined
                  rounded
                  v-model="cedula"
                  :rules="[rules.cedula, rules.counter, rules.required, rules.ced]"
                  counter
                  maxlength="10"
                  color="primary"
                >
                </v-text-field>

                <v-text-field
                  v-model="fechaNacimiento"
                  label="Fecha de Nacimiento"
                  outlined
                  rounded
                  type="date"
                ></v-text-field>
                <v-text-field
                  ref="telefono"
                  label="Teléfono"
                  outlined
                  rounded
                  v-model="telefono"
                  :rules="[rules.tel, rules.counter, rules.required]"
                  counter
                  maxlength="10"
                  color="primary"
                >
                </v-text-field>
                <v-select
                  :items="generos"
                  label="Género"
                  outlined
                  rounded
                  v-model="genero"
                  :rules="[() => !!genero || 'Campo obligatorio']"
                ></v-select>
                <v-text-field
                  ref="correo"
                  label="Correo electrónico"
                  outlined
                  rounded
                  v-model="correo"
                  type="email"
                  :rules="[rules.email, rules.required]"
                  color="primary"
                >
                </v-text-field>
              </v-form>
            </v-card-text>

            <v-btn
              id="btn-ingreso"
              color="secondary"
              :disabled="!valid"
              @click="enviarCon"
            >
              Agregar
            </v-btn>
          </v-col>
        </v-row>
      </div>

      <v-layout align-start>
        <v-flex>
          <!-- Tabla en la que listo los esttudiantes -->
          <v-data-table
            :headers="headers"
            :items="desserts"
            :search="search"
            class="elevation-1"
          >
            <template v-slot:top>
              <v-toolbar flat>
                <v-toolbar-title>Lista de Estudiantes</v-toolbar-title>
                <v-divider class="mx-4" inset vertical></v-divider>
                <v-spacer></v-spacer>
                <v-text-field
                  class="text-xs-center"
                  v-model="search"
                  append-icon-cb="search"
                  label="Buscar"
                  single-line
                  hide-details
                >
                </v-text-field>
                <v-spacer></v-spacer>
                <!-- //DIALOGO DE EDITAR ESTUDIANTES -->
                <v-dialog v-model="dialog" max-width="500px">
                  <v-card>
                    <v-card-text>
                      <v-container>
                        <v-row>
                          <v-col cols="12" sm="6" md="6">
                            <v-text-field
                              v-model="nombres"
                              label="Nombres"
                              :rules="[() => !!nombres || 'Campo obligatorio']"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="6">
                            <v-text-field
                              v-model="apellidos"
                              label="Apellidos"
                              :rules="[
                                () => !!apellidos || 'Campo obligatorio',
                              ]"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="6">
                            <v-text-field
                              v-model="cedula"
                              :rules="[rules.required, rules.counter, rules.cedula, rules.ced]"
                              counter
                              maxlength="10"
                              color="primary"
                              label="Cédula"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="6">
                            <v-text-field
                              v-model="fechaNacimiento"
                              label="Fecha de Nacimiento"
                              type="date"
                              :rules="[
                                () => !!fechaNacimiento || 'Campo obligatorio',
                              ]"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="6">
                            <v-text-field
                              v-model="correo"
                              label="Correo electrónico"
                              :rules="[rules.required, rules.email]"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="6">
                            <v-text-field
                              v-model="telefono"
                              label="Teléfono"
                              :rules="[rules.required, rules.counter, rules.tel]"
                              counter
                              maxlength="10"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="6">
                            <v-select
                              :items="generos"
                              label="Género"
                              v-model="genero"
                              :rules="[() => !!genero || 'Campo obligatorio']"
                            ></v-select>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-card-text>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="blue darken-1" text @click="close">
                        Cancelar
                      </v-btn>

                      <v-btn color="blue darken-1" text> Editar </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
                <v-dialog v-model="dialogDelete" max-width="500px">
                  <v-card>
                    <v-card-title class="text-h7"
                      >¿Estás seguro que deseas borrar el
                      registro?</v-card-title
                    >
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="blue darken-1" text @click="closeDelete"
                        >Cancelar</v-btn
                      >
                      <v-btn color="blue darken-1" text>Aceptar</v-btn>
                      <v-spacer></v-spacer>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </v-toolbar>
            </template>
            <template v-slot:[`item.actions`]="{ item }">
              <v-icon small class="mr-2" @click="editItem(item)">
                mdi-pencil
              </v-icon>
              <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
            </template>
            <template v-slot:no-data>
              <v-btn color="primary"> No hay registros </v-btn>
            </template>
            <template v-slot:[`item.esControlador`]="{ item }">
              <p style="margin-top: 5px" v-if="!item.esControlador">
                <v-chip class="ma-2" color="green" outlined>
                 Administrador
                </v-chip>
              </p>
              <p style="margin-top: 5px" v-else>
                <v-chip class="ma-2" color="orange" outlined>
                  Controlador
                </v-chip>
              </p>
            </template>

          </v-data-table>
        </v-flex>
      </v-layout>
    </v-responsive>
  </v-card>
</template>

<script>
import axios from "axios";
export default {
  layout: "admin",

  data() {
    return {
      valid: true,
      facul: "",
      sadmin: false,
      scon: false,
      rules: {
        required: (value) => !!value || "Campo Requerido.",

        counter: (value) => value.length == 10 || "Se requiere 10 dígitos",
        ced: (value) => {
          const pattern = /^[0-9]*$/;
          return pattern.test(value) || "Solo números";
        },
        tel: (value) => {
          const pattern = /^([0])+(9)+([0-9])*$/;
          return pattern.test(value) || "No es un número telefónico válido";
        },
        email: (value) => {
          const pattern =
            /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
          return pattern.test(value) || "No es un correo válido.";
        },
        cedula: (value) =>this.validar(value) || "Cédula inválida"
      },

      generos: ["Masculino", "Femenino"],

      cedula: "",
      nombres: "",
      apellidos: "",
      fechaNacimiento: "", //localDate
      correo: "",
      usuario: "",
      telefono: "",

      genero: "",
      esControlado1: true,
      esControlado: false,

      dialog: false,
      dialogDelete: false,
      // id: "",
      // departamentoProducto: "",
      // impactoExterno: "",
      // impactoInterno: "",

      headers: [
        {
          text: "Nombres",
          value: "nombres",
        },
        {
          text: "Apellidos",
          value: "apellidos",
        },
        {
          text: "Cédula",
          value: "cedula",
          sortable: true,
        },
        {
          text: "Fecha de Nacimiento",
          value: "fechaNacimiento",
        },
        {
          text: "Género",
          value: "genero",
        },
        {
          text: "Correo",
          value: "correo",
        },
        {
          text: "Teléfono",
          value: "telefono",
        },

        {
          text: "Usuario",
          value: "usuario",
        },
        {
          text: "Rol",
          value: "esControlador",
        },
        {
          text: "Identificador",
          value: "identificadorAdmin",
        },
      ],
      search: "",
      desserts: [],
      editedIndex: -1,
      // editedItem: {
      //   departamentoProducto: "",
      //   impactoExterno: "",
      //   impactoInterno: "",
      // },
      // defaultItem: {
      //   departamentoProducto: "",
      //   impactoExterno: "",
      //   impactoInterno: "",
      // },
    };
  },
  mounted() {
    this.obtenerListaAdmin();
    // this.sesion();
    // this.obtenerFac();
  },
  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "Nuevo Registro" : "Editar Registro";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
    facul: function () {
      this.prueba.forEach((elementos) => {
        if (elementos.nombre === this.facul) {
          this.listaCarreras = elementos.carreras;
        }
      });
    },
  },

  methods: {
    validar(cedula) {
      //var cedula = document.getElementById("ced").value.trim();
      console.log(cedula);

      //Preguntamos si la cedula consta de 10 digitos
      if (cedula.length == 10) {
        //Obtenemos el digito de la region que sonlos dos primeros digitos
        var digito_region = cedula.substring(0, 2);

        //Pregunto si la region existe ecuador se divide en 24 regiones
        if (digito_region >= 1 && digito_region <= 24) {
          // Extraigo el ultimo digito
          var ultimo_digito = cedula.substring(9, 10);

          //Agrupo todos los pares y los sumo
          var pares =
            parseInt(cedula.substring(1, 2)) +
            parseInt(cedula.substring(3, 4)) +
            parseInt(cedula.substring(5, 6)) +
            parseInt(cedula.substring(7, 8));

          //Agrupo los impares, los multiplico por un factor de 2, si la resultante es > que 9 le restamos el 9 a la resultante
          var numero1 = cedula.substring(0, 1);
          var numero1 = numero1 * 2;
          if (numero1 > 9) {
            var numero1 = numero1 - 9;
          }

          var numero3 = cedula.substring(2, 3);
          var numero3 = numero3 * 2;
          if (numero3 > 9) {
            var numero3 = numero3 - 9;
          }

          var numero5 = cedula.substring(4, 5);
          var numero5 = numero5 * 2;
          if (numero5 > 9) {
            var numero5 = numero5 - 9;
          }

          var numero7 = cedula.substring(6, 7);
          var numero7 = numero7 * 2;
          if (numero7 > 9) {
            var numero7 = numero7 - 9;
          }

          var numero9 = cedula.substring(8, 9);
          var numero9 = numero9 * 2;
          if (numero9 > 9) {
            var numero9 = numero9 - 9;
          }

          var impares = numero1 + numero3 + numero5 + numero7 + numero9;

          //Suma total
          var suma_total = pares + impares;

          //extraemos el primero digito
          var primer_digito_suma = String(suma_total).substring(0, 1);

          //Obtenemos la decena inmediata
          var decena = (parseInt(primer_digito_suma) + 1) * 10;

          //Obtenemos la resta de la decena inmediata - la suma_total esto nos da el digito validador
          var digito_validador = decena - suma_total;

          //Si el digito validador es = a 10 toma el valor de 0
          if (digito_validador == 10) var digito_validador = 0;

          //Validamos que el digito validador sea igual al de la cedula
          if (digito_validador == ultimo_digito) {
           // document.getElementById("salida").innerHTML = "Cedula Válida";
           return true;
          } else {
            //document.getElementById("salida").innerHTML = "Cedula Inválida";
            return false;
            
          }
        } else {
          // imprimimos en consola si la region no pertenece
            return false;
        }
      } else {
        //imprimimos en consola si la cedula tiene mas o menos de 10 digitos
       // document.getElementById("salida").innerHTML =
          //"Cedula Invalida contiene menos digitos";
          return false;
      }
    },
     async calculateAge() {
      var d = document.getElementById("user_date").value;
      var inDate = new Date(d);
      var anio = inDate.getFullYear();
      var fec_actual = new Date();
      var fec_anio = fec_actual.getFullYear();
      var edad = fec_anio - anio;
      if (edad >= 16) {
       this.enviar();

      } else {
        this.$notifier.showMessage({
            content: `Ingrese una edad válida`,
            color: "warning",
          });
      }
    },
    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.desserts.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    // guardarMod() {
    //   if (this.editedIndex > -1) {
    //     Object.assign(this.desserts[this.editedIndex], this.editedItem);
    //   } else {
    //     this.desserts.push({
    //       departamentoProducto: this.editedItem.departamentoProducto,
    //       impactoInterno: this.editedItem.impactoInterno,
    //       impactoExterno: this.editedItem.impactoExterno,
    //     });
    //   }
    //   this.close();
    // },
    // async actualizarDat() {
    //   try {
    //     const datos = {
    //       user: this.$cookies.get("dataClient").usuario.nombreUsuario,
    //       departamentoProducto: this.editedItem.departamentoProducto,
    //       impactoInterno: this.editedItem.impactoInterno,
    //       impactoExterno: this.editedItem.impactoExterno,
    //     };

    //     await this.$axios.put(
    //       `api/sgcnegocio/formularioImpactoComparativo/actualizarImpacto/${this.editedItem.id}`,
    //       datos
    //     );
    //     this.guardarMod();
    //   } catch (err) {
    //     console.log(err);
    //   }
    // },

    async obtenerListaAdmin() {
      try {
        const res = await axios.get("api/administrador", {
          headers: {
            authorization: "SGVUCE " + this.$cookies.get("ROLE_ADMIN"),
          },
        });

        this.desserts = res.data;
       
      } catch (err) {
        console.log(err);
        if (err.response.status == 403) {
          this.$cookies.remove("ROLE_ADMIN");
          this.$notifier.showMessage({
            content: `Su sesión ha expirado`,
            color: "error",
          });
          this.$router.push("/login");
        }
        // this.$cookies.set('ROLE_ADMIN', respuesta.data.token_actualizado);

        // this.$router.push("/login");
   

      }
    },

  

    llenarTabla() {
      this.desserts.push({
        nombres: this.nombres,
        apellidos: this.apellidos,
        cedula: this.cedula,
        correo: this.correo,
        fechaNacimiento: this.fechaNacimiento,

        telefono: this.telefono,
        genero: this.genero,
      });
      this.obtenerListaAdmin();
    },

    async enviar() {
      if (
        !this.nombres ||
        !this.apellidos ||
        !this.fechaNacimiento ||
        !this.cedula ||
        !this.correo ||
        !this.telefono ||
        !this.genero
      ) {
        this.$notifier.showMessage({
          content: "Rellene todos los datos",
          color: "error",
        });
      } else {
        try {
          const res = await this.$axios.post(
            "api/administrador/crearAdmin",
            {
              nombres: this.nombres.trim(),
              apellidos: this.apellidos.trim(),
              fechaNacimiento: this.fechaNacimiento,
              cedula: this.cedula.trim(),
              correo: this.correo.trim(),
              telefono: this.telefono.trim(),
              genero: this.genero,

              esControlador: this.esControlado,
            },
            {
              headers: {
                authorization: "SGVUCE " + this.$cookies.get("ROLE_ADMIN"),
              },
            },
            this.correo.trim(),
            (this.nombres = " "),
            (this.apellidos = " "),
         
            (this.cedula = " "),
            (this.correo = " "),
            (this.telefono = " "),
            (this.genero = " ")
          
          );
          this.llenarTabla(),
            this.$notifier.showMessage({
              content: "Administrador añadido con éxito",
              color: "success",
            });
          console.log(res);
        } catch (err) {
          console.log(err);
             if (err.response.data.mensaje == "Request processing failed; nested exception is java.lang.ArrayIndexOutOfBoundsException: Index 1 out of bounds for length 1") {
            this.$notifier.showMessage({
              content: "Debe ingresar dos apellidos",
              color: "warning",
            });
          } else if (err.response.status == 500) {
            this.$notifier.showMessage({
              content: "Cédula o Correo Duplicados",
              color: "warning",
            });
          }
        }
      }
    },
    async enviarCon() {
      if (
        !this.nombres ||
        !this.apellidos ||
        !this.fechaNacimiento ||
        !this.cedula ||
        !this.correo ||
        !this.telefono ||
        !this.genero
      ) {
        this.$notifier.showMessage({
          content: "Rellene todos los datos",
          color: "error",
        });
      } else {
        try {
          const res = await this.$axios.post(
            "api/administrador/crearControlador",
            {
              nombres: this.nombres,
              apellidos: this.apellidos,
              fechaNacimiento: this.fechaNacimiento,
              cedula: this.cedula,
              correo: this.correo,
              telefono: this.telefono,
              genero: this.genero,

              esControlador: this.esControlado1,
            },
            {
              headers: {
                authorization: "SGVUCE " + this.$cookies.get("ROLE_ADMIN"),
              },
            },
            this.correo.trim(),
            (this.nombres = " "),
            (this.apellidos = " "),
            (this.cedula = " "),
            (this.correo = " "),
            (this.telefono = " "),
            (this.genero = " ")
          );
          this.llenarTabla(),
            this.$notifier.showMessage({
              content: "Controlador añadido con éxito",
              color: "success",
            });
          console.log(res);
        } catch (err) {
          console.log(err);
             if (err.response.data.mensaje == "Request processing failed; nested exception is java.lang.ArrayIndexOutOfBoundsException: Index 1 out of bounds for length 1") {
            this.$notifier.showMessage({
              content: "Debe ingresar dos apellidos",
              color: "warning",
            });
          } else if (err.response.status == 500) {
            this.$notifier.showMessage({
              content: "Cédula o Correo Duplicados",
              color: "warning",
            });
          }
        }
      }
    },
  },
};
</script>
<style >
.imagen {
  margin-left: 35%;
  width: 30%;
}
#btn-ingreso {
  margin-top: 2%;
  margin-left: 40%;
}
</style>