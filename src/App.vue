<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-row>
            <v-col cols="12" sm="6" md="3">
            <v-text-field
              v-on:keydown.enter="addTask"
              v-model="aufgabe"
              label="Aufgabe eingeben"
            ></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="3">
              <v-text-field
                v-on:keydown.enter="addTask"
                v-model="uhrzeit"
                label="Uhrzeit"
              ></v-text-field>
            </v-col>
            <v-col cols="12" sm="6" md="3">
              <v-date-picker v-model="datum"></v-date-picker>
            </v-col>

            <v-row align="center" justify="space-around">
              <v-btn v-on:click="addTask"> Aufgabe hinzufügen </v-btn>
            </v-row>
            <v-card class="mx-auto" max-width="900" tile>
              <v-list dense>
                <v-subheader>Aufgabenliste</v-subheader>
                <v-list-item-group color="primary">
                  <div v-for="(teilaufgabe, i) in aufgabeliste" :key="i">
                    <v-list-item
                      v-if="
                        teilaufgabe.time > realTime && teilaufgabe.day > realday">
                      <v-list-item-content>
                        <v-list-item-title
                          v-text="
                            teilaufgabe.time +
                            ' ' +
                            teilaufgabe.name +
                            ' ' +
                            teilaufgabe.day
                          "
                        ></v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                  </div>
                </v-list-item-group>
              </v-list>
            </v-card>
          </v-row>  
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>
// before und after zum DAtumsvergleich 
// mit typescript
// timepicker



<script>
export default {
  name: "App",

  data() {
    return {
      aufgabe: "",
      name: "",
      uhrzeit: "",
      datum: "",
      aufgabeliste: [],
      realTime: new Date().toLocaleTimeString(),
      realday: new Date(),
    };
  },

  methods: {
    addTask() {
      console.log(this);
      this.datum = new Date(this.datum)
      if (
        this.aufgabe.length > 0 &&
        this.uhrzeit.length > 0) {
      //else (      )   
        const task = {
          name: this.aufgabe,
          time: this.uhrzeit,
          day: this.datum,
        };
        this.aufgabeliste.push(task)
        this.aufgabe = ""
        this.uhrzeit = ""
        this.datum = ""
      }
      console.log(this.aufgabeliste)
      console.log(this.realday)
      console.log(this.datum)
      console.log(this.datum > this.realday)
    },
  },
};
</script>
