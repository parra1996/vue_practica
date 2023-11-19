<template>
   <v-dialog width="500" >
      <template v-slot:activator="{ props }">
        <v-btn v-bind="props" text="Open Dialog"> </v-btn>
      </template>

      <template v-slot:default="{ isActive }">
        <v-card title="Dialog">
        
        <v-form v-model="valid" @submit.prevent="submit">
        <v-container>
          <v-row>
            <v-col
              cols="12"
              md="4"
            >
              <v-text-field
                v-model="firstname"
                :rules="nameRules"
                :counter="10"
                label="First name"
                required
                hide-details
              ></v-text-field>
            </v-col>

            <v-col
              cols="12"
              md="4"
            >
              <v-text-field
                v-model="lastname"
                :rules="nameRules"
                :counter="10"
                label="Last name"
                hide-details
                required
              ></v-text-field>
            </v-col>

            <v-col
              cols="12"
              md="4"
            >
              <v-text-field
                v-model="email"
                :rules="emailRules"
                label="E-mail"
                hide-details
                required
              ></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-form>

       <v-card-actions>
            <v-spacer></v-spacer> 

            <v-btn
              text="Close Dialog"
              @click="isActive.value = false; submit()"
            ></v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
</template>

<script>
export default {
    emits: ['formData'],
    data: () => ({
        valid: false,
        firstname: '',
        lastname: '',
        nameRules: [
            value => {
                if (value) return true;

                return 'Name is required.';
            },
            value => {
                if (value?.length <= 10) return true;

                return 'Name must be less than 10 characters.';
            },
        ],
        email: '',
        emailRules: [
            value => {
                if (value) return true;

                return 'E-mail is requred.';
            },
            value => {
                if (/.+@.+\..+/.test(value)) return true;

                return 'E-mail must be valid.';
            },
        ],
    }),
    methods: {
        submit(){
            const data = [];
            data.firstname = this.firstname
            data.lastname = this.lastname
            data.email = this.email
            this.$emit('formData', data )
        }
    },
};
</script>