<template>
  <div class="about">
      
    <table class="dataTable">
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Text</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="data in tab" v-bind:key="data.id">
          <td scope="row">{{ data.id }}</td>
          <td scope="row">{{ data.text }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Login",

  components: {
    
  },

  data() {
    
    return {
      //title: "home",            
      
      tab: [],
    };
  },

  computed: {
    
  },

  created() {
    
    this.getDataAction();
  },

  methods: {
    
        getDataAction() {
          
      axios
        .get("https://otthoni-feladat-backend.herokuapp.com/data" , {
          headers: {
            "x-api-key": localStorage.token,
          },
        })
        .then((response) => {
          this.tab = response.data;
          console.log(response.data);
          
          console.log(this.tab);
          localStorage.clear();   // A localStorage törlése, hogy ne lehessen megkerülni a logint.
        })
        .catch((error) => {
          if (error.response) {
            alert(error.response.data);
          }
        });
    },
  },
};
</script>

<style scoped>

.dataTable thead tr {
  background-color: #009879;
  color: white;
  text-align: left;
  font-weight: bold;
}

.dataTable {
    border-collapse: collapse;
    margin-top: 200px;
    font-size: 1.2rem;
    min-width: 250px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
    border-radius: 5px 5px 0 0;
    overflow: hidden;
    margin-left: auto;
    margin-right: auto;
}

.dataTable th, td {
  padding: 12px 10px;
  text-align: left;
}

.dataTable tbody tr {
  border-bottom: 1px solid #dddddd;
}

.dataTable tbody tr:last-of-type {
  border-bottom: 2px solid #009879;
}
</style>>
