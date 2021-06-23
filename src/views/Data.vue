<template>
  <div class="about">
      <!-- A V-for-al végig tudunk lépkedni a tömbünk elemein, de kell neki egy azonosító is (v-bind:key)-->
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
    //Objektum, ebbe fogjuk megadni azokat a komponenseket, amiket az About használ
  },

  data() {
    //Függvény, ami egy objektumot ad vissza. A komponens betöltésekor értékeli ki. STATIKUS adatok vannak benne.
    return {
      //title: "home",            //A template-ban tudunk rá hivatkozni így pl.: <p>{{title}}</p>
      
      tab: [],
    };
  },

  computed: {
    //Objektum, ezen belül tudunk függvényeket meghatározni. Amelyek figyelni fognak a változásokra is.
    //Ha DINAMIKUS adatra van szükség akkor azt itt kell használni.
  },

  created() {
    //Életciklus hook. A komponens létrehozásakor fut le. Itt szokás beállítani különböző értékeket, amikre szükségünk van.
    //Lefut minden egyes alkalommal, amikor a komponens létre jön.
    this.getDataAction();
  },

  methods: {
    // Objektum.  Különböző függvényeket tudunk benne definiálni, amiket a komponensünk fog tudni használni.
        getDataAction() {
          console.log("FUTOOOK");
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