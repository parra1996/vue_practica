<template>
    appvue
    <Dialog @formData="getMethod"/>

      <v-table v-if="users.length > 0">
        <thead>
          <tr>
            <th class="text-left">
              Name
            </th>
            <th class="text-left">
              lastname
            </th>
            <th class="text-left">
              email
            </th>
            <th class="text-left">
              change Data
            </th>
          </tr>
        </thead>
        <tbody>
            <tr
                v-for="user in users"
                :key="user.firstname"
            > 
                <td>{{ user.firstname }}</td>
                <td>{{ user.lastname }}</td>
                <td>{{ user.email }}</td>
                <td>
                    <Dialog @formData="getMethod"/>
                </td>
                <td @click="deleteUser(user.firstname)">
                    eliminar
                </td> 
            </tr>
        </tbody>
      </v-table>
    </template>

<script>
import Dialog from './views/Dialog.vue';
export default {
    components:{
        Dialog
    },
    data(){
        return {
            userInfo: {},
            showTab: false,
            users: []
          
        }
    },
    methods: {
        getMethod(data){
            console.log("entramos al getmethod")
            console.log(data)
            this.users.push(data)
        },
        deleteUser(user){
            console.log(user)
            
        }
    }
}
</script>