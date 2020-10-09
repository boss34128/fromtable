<template>
  <div>
    <h2>Hotel room booking</h2>
    <v-card class="mx-auto pa-6" color="#117c00" max-width="900" elevation="15">
      <h3>Customer details</h3>
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-row>
          <v-col cols="7">
            <v-text-field
              v-model="name"
              :rules="nameRules"
              label="Name-Surname"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="5">
            <v-text-field
              v-model="phone"
              :rules="nameRules"
              label="Phone number"
              prepend-icon="mdi-cellphone"
              required
            >
              icon="mdi-cellphone"
            </v-text-field>
          </v-col>
        </v-row>
        <v-text-field
          v-model="email"
          :rules="emailRules"
          label="E-mail"
          prepend-icon="mdi-email"
          required
        ></v-text-field>
        <v-row>
          <v-col cols="6">
            <v-text-field
              v-model="add"
              :rules="nameRules"
              name="input-7-1"
              label="Address"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="6">
            <v-text-field
              v-model="sub_district"
              :rules="nameRules"
              name="input-7-1"
              label="Tombon"
              required
            ></v-text-field> </v-col
        ></v-row>
        <v-row
          ><v-col cols="6">
            <v-text-field
              v-model="district"
              :rules="nameRules"
              name="input-7-1"
              label="Amphoe"
              required
            ></v-text-field
          ></v-col>
          <v-col cols="6">
            <v-text-field
              v-model="province"
              :rules="nameRules"
              name="input-7-1"
              label="Province"
              required
            ></v-text-field>
          </v-col>
        </v-row>

        <v-divider></v-divider>
        <h3>Booking details</h3>
        <v-row>
          <v-col cols="6" sm="6">
            <v-menu
              ref="menu"
              v-model="menu2"
              :rules="nameRules"
              :dateout-on-content-click="false"
              :nudge-right="40"
              :return-value.sync="datein"
              transition="scale-transition"
              offset-y
              max-width="290px"
              min-width="290px"
            >
              <template v-slot:activator="{ on, attrs }">
                <v-text-field
                  v-model="datein"
                  :rules="nameRules"
                  label="Date"
                  prepend-icon="mdi-table-large"
                  readonly
                  required
                  v-bind="attrs"
                  v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker
                v-if="menu2"
                v-model="datein"
                full-width
                @click:date="$refs.menu.save(datein)"
              ></v-date-picker>
            </v-menu>
          </v-col>

          <v-col cols="6" sm="6">
            <v-menu
              ref="menu1"
              v-model="menu1"
              :dateout-on-content-click="false"
              :nudge-right="40"
              :return-value.sync="dateout"
              transition="scale-transition"
              offset-y
              max-width="290px"
              min-width="290px"
            >
              <template v-slot:activator="{ on, attrs }">
                <v-text-field
                  v-model="dateout"
                  :rules="nameRules"
                  label="Up to date"
                  prepend-icon="mdi-table-large"
                  readonly
                  required
                  v-bind="attrs"
                  v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker
                v-if="menu1"
                v-model="dateout"
                full-width
                @click:date="$refs.menu1.save(dateout)"
              ></v-date-picker>
            </v-menu>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="6">
            <v-select
              v-model="room"
              :rules="nameRules"
              :items="items"
              prepend-icon="mdi-home-outline"
              label="Number of rooms"
              required
            ></v-select>
          </v-col>
          <v-col cols="6">
            <v-select
              v-model="costumers"
              :rules="nameRules"
              :items="kon"
              prepend-icon="mdi-home-outline"
              label="Number of people"
              required
            ></v-select>
          </v-col>
        </v-row>
        <v-divider></v-divider>

        <v-row>
          <v-col cols="10"> </v-col>
          <v-col cols="2">
            <div class="text-center">
              <v-dialog v-model="dialog" width="800">
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    depressed
                    color="#00ff78"
                    :disabled="!valid"
                    v-bind="attrs"
                    v-on="on"
                    @click="validate"
                  >
                    SUMMIT
                  </v-btn>
                </template>

                <v-card class="pa-4" elevation="11">
                  <v-row>
                    <v-col cols="12"> Confirm information </v-col>
                  </v-row>

                  <v-divider></v-divider>
                  <v-card-text
                    ><h4>
                      Name: {{ name }} <br />
                      Phone Number: {{ phone }} <br />
                      E-mail: {{ email }} <br />
                      Address: {{ add }} Tombon {{ sub_district }} Amphoe
                      {{ district }} Province {{ province }} <br />
                      Since {{ datein }} Up to date {{ dateout }}<br />
                      Number of {{ costumers }} People {{ room }} Room
                    </h4></v-card-text
                  >

                  <v-divider></v-divider>

                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="primary" text @click="dialog = false">
                      Edit
                    </v-btn>
                    <v-btn
                      color="primary"
                      text
                      @click=";(dialog = false), set(), reset()"
                    >
                      Confirm
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </div>
          </v-col>
        </v-row>
      </v-form>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: null,
      phone: '',
      add: '',
      Address: {},
      room: '',
      email: '',
      costumers: '',
      kon: [1, 2, 3, 4, 5, 6],
      items: [1, 2, 3, 4, 5, 6],
      arr: {},
      description: '',
      datein: '',
      dateout: '',
      menu1: false,
      menu2: false,
      sub_district: '',
      district: '',
      province: '',
      dialog: false,
      nameRules: [(v) => !!v || 'please required'],
      emailRules: [
        (v) => !!v || 'E-mail is required',
        (v) => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
      valid: true,
    }
  },
  methods: {
    reset() {
      this.$refs.form.reset()
    },
    validate() {
      this.$refs.form.validate()
    },
    set() {
      this.arr = {
        name: this.name,
        email: this.email,
        room: this.room,
        costumers: this.costumers,
        phone: this.phone,
        address: {
          add: this.add,
          sub_district: this.sub_district,
          district: this.district,
          province: this.province,
        },
        description: this.description,
        date_in: this.datein,
        date_out: this.dateout,
        sub_district: this.sub_district,
        district: this.district,
        province: this.province,
      }
      this.$store.commit('set_arr', this.arr)
    },
  },
}
</script>
