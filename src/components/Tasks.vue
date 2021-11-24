<template>
  <v-container>
    <v-row class="d-flex justify-center">
      <v-col cols="12" sm="9" md="6">
        <v-card color="theme--dark" dark>
          <v-container class="d-flex flex-column">
            <v-row class="ma-sm-4">
              <v-col cols="8" class="d-flex flex-row">
                <h1 class="text-h3 text-sm-h2 font-weight-bold d-flex align-center">{{ dia }}</h1>
                <div class="d-flex flex-column mx-1">
                  <p class="text-subtitle-1 text-sm-h6 font-weight-bold ma-0">{{ mes }}</p>
                  <p class="text-subtitle-1 text-sm-h6 ma-0">{{ anio }}</p>
                </div>
              </v-col>
              <v-col cols="4" class="d-flex justify-end">
                <h3
                  class="text-subtitle-1 text-sm-h6 font-weight-bold d-flex align-center">{{ diaL }}</h3>
              </v-col>
            </v-row>
            <v-row class="my-0 d-flex flex-row align-center">
              <v-col cols="9">
                <v-text-field color="indigo" label="Nueva tarea" v-model="note"></v-text-field>
              </v-col>
              <v-col cols="3" class="d-flex justify-center">
                <v-btn @click="add(note)" fab dark small color="indigo">
                  <v-icon dark>mdi-plus</v-icon>
                </v-btn>
              </v-col>
            </v-row>
            <v-row class="d-flex flex-column justify-center">
              <v-list rounded three-line flat class="mx-2">
                <v-list-item-group multiple>
                  <v-list-item dark v-for="(item, i) in items" :key="i" :class="{'indigo':items[i].isCompleted}">
                    <v-list-item-icon class="ma-auto">
                      <v-icon @click="isTaskCompleted(i)" v-text="iconCompleted(i)"></v-icon>
                    </v-list-item-icon> 
                    <v-list-item-content class="ml-2">
                      <router-link :to="{name: 'Task', params: {id:item}}">
                        <v-list-item-title v-text="item.title"></v-list-item-title>
                        <v-list-item-subtitle v-text="item.description"></v-list-item-subtitle>  
                      </router-link>
                    </v-list-item-content>
                    <v-list-item-icon class="ma-auto">
                      <v-icon @click="taskDelete(i)">mdi-trash-can</v-icon>
                    </v-list-item-icon> 
                  </v-list-item>
                </v-list-item-group>
              </v-list>
            </v-row>
            <v-row>
              <v-btn text> Listen Now </v-btn>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: "tasks",
  data: function () {
    return {
      note: '',
      dia: "",
      mes: "",
      anio: "",
      diaL: "",
      selectedItem: 1,
      items: [
        { title: 'Real-Time', description: 'Description', isCompleted: false },
        { title: 'Audience', description: 'Description Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas praesentium fugit doloremque rerum impedit at consequaturs.', isCompleted: false },
      ],
    };
  },
  methods: {
    cargarFechaActual() {
      const meses = new Array(
        "Ene",
        "Feb",
        "Mar",
        "Abr",
        "May",
        "Jun",
        "Jul",
        "Ago",
        "Sept",
        "Oct",
        "Nov",
        "Dic"
      );
      const diasSemana = new Array(
        "Domingo",
        "Lunes",
        "Martes",
        "Miércoles",
        "Jueves",
        "Viernes",
        "Sábado"
      );
      const f = new Date();
      this.dia = f.getDate();
      this.mes = meses[f.getMonth()];
      this.anio = f.getFullYear();
      this.diaL = diasSemana[f.getDay()];
    },
    isTaskCompleted(i){
      this.items[i].isCompleted = !this.items[i].isCompleted
    },
    iconCompleted(i){
      if (this.items[i].isCompleted) {
        return 'mdi-note-check'
      }else{
        return 'mdi-note-alert'
      }
    },
    taskDelete(i){
      this.items.splice(i,1)
    },
    add(titleM){
      if (titleM !== '') {
        let task = { title: titleM, description: 'Description', isCompleted: false}
        this.items.push(task)
        this.note=''
      }else{
        alert('El titulo no puede estar vacio')
      }
    }
  },
  created() {
    this.cargarFechaActual();
  },
};
</script>
<style scoped>
  a  {
    text-decoration: none;
  }
</style>