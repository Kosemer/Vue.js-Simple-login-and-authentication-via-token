<template>
  <div id="app">
    <div id="nav">
      <router-link to="/"></router-link> 
      <router-link to="/Data"></router-link>
    </div>
    <router-view/>
  </div>
</template>

<script>

export default {
  name: "Login",

  components: {
    //Objektum, ebbe fogjuk megadni azokat a komponenseket, amiket a Home használ
  },

  data() {
    //Függvény, ami egy objektumot ad vissza. A komponens betöltésekor értékeli ki. STATIKUS adatok vannak benne.
    return {
      //title: "home",            //A template-ban tudunk rá hivatkozni így pl.: <p>{{title}}</p>

    };
  },

  computed: {
    //Objektum, ezen belül tudunk függvényeket meghatározni. Amelyek figyelni fognak a változásokra is.
    //Ha DINAMIKUS adatra van szükség akkor azt itt kell használni.
  },

  created() {
    //Életciklus hook. A komponens létrehozásakor fut le. Itt szokás beállítani különböző értékeket, amikre szükségünk van.
    //Lefut minden egyes alkalommal, amikor a komponens létre jön.
  },

  methods: {
    // Objektum.  Különböző függvényeket tudunk benne definiálni, amiket a komponensünk fog tudni használni.


  },
};
</script>


<style>

</style>
