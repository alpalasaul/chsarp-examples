<template>
  <v-card>
    <v-responsive :aspect-ratio="16 /9">
      <h1
        style="text-align: center; margin-bottom: 10px"
      >Bienvenido al Sistema de Gestión de Vacunación Uce</h1>
      <img class="imagen" src="/IngresoAdmin.svg" />
       <br/>
        <br/>
      <v-card-text>
        <div class="card">
          <div class="container" id="tamaño">
            <v-card-text class="texto">
              Como Universidad Central del Ecuador nos hemos sumado a esta
                lucha hombro a hombro para poder hacerle
              
                frente al virus, a través de la inoculación de la comunidad educativa, siendo los estudiantes
                los usuarios que
              
                accederán a las brigadas de vacunación, la cual se llevará acabo en las instalaciones
                de la Universidad
              Central del Ecuador. </v-card-text>
              <v-card-text>Este sistema fue creado con el fin de ser un soporte a la
          al Ministerio de Salud del Ecuador y al país, en el sistema de vacunación que actualmente se esta
          llevando acabo en todo el país. </v-card-text>

          </div>
        </div>
        <br />
         <br />
        <br />
          <br />
        <br />
        

        <h3 style="text-align: center; margin-bottom: 10px">Gracias por formar parte de este equipo</h3>
        <h1 style="text-align: center; margin-bottom: 10px">Juntos Saldremos de esto</h1>

        <br />

        <img class="ministerio" src="/ministerioSalud.png" />
        <img style="right " class="uce" src="/uce.jpeg" />
      </v-card-text>
    </v-responsive>
  </v-card>
</template>
<script>
export default {
  layout: "admin",
};
</script>
<style >
.imagen {
  margin-left: 40%;
  width: 60%;
}
.ministerio {
  margin-left: 25%;
  width: 15%;
}
.uce {
  margin-left: 15%;
  width: 20%;
}
.texto {
  text-align: justify;
  align-content: "center";
}

.card {
  /* Add shadows to create the "card" effect */
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
   margin-left: 15%;
  width: 70%;
}

/* On mouse-over, add a deeper shadow */
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}

/* Add some padding inside the card container */
.container {
  padding: 2px 16px;
  
}
</style>