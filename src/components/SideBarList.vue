<template>
  <div class="sideBarList">
    <div class="ui visible left vertical sidebar menu">
      <a class="item" v-for="country in countries.data" :key="country.id" @click="CountrySelected(country.name)">
        <img class="ui avatar image" :src="country.flag" alt>
        {{ country.name }}
      </a>
    </div>
    <div class="pusher">
      <div class="ui center aligned page grid">
        <div v-if="countrySelectedList" class="countryTable">
          <h1
            class="ui header center aligned page grid"
            style="font-size: 40px; padding-right:20px;"
          >{{ countryName }}</h1>
          <table class="ui selectable inverted fixed celled table column twelve wide">
            <thead>
              <tr>
                <th class="three wide">Capital</th>
                <th class="three wide">Región</th>
                <th class="three wide">Gentilicio</th>
                <th class="three wide">Nombre Nativo</th>
              </tr>
            </thead>
            <tbody v-for="countrySelected in countrySelectedList.data" :key="countrySelected.id">
              <tr>
                <td>{{ countrySelected.capital }}</td>
                <td>{{ countrySelected.region }}</td>
                <td>{{ countrySelected.demonym }}</td>
                <td>{{ countrySelected.nativeName }}</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="travelersBackground" v-else>
          <img
            src="https://cdn2.traveler.es/uploads/images/thumbs/es/trav/3/s/2018/28/un_fin_de_semana_para_viajar_o_para_disfrutar_de_la_ciudad_llena_de_planes_diferentes_6962_940x627.jpg"
            alt
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SideBarList",
  created() {
    axios
      .get("https://restcountries.eu/rest/v2/")
      .then(response => (this.countries = response));
  },
  data() {
    return {
      countries: null,
      countrySelectedList: null,
      countryName: null
    };
  },
  methods: {
    CountrySelected(countryName) {
      axios
        .get("https://restcountries.eu/rest/v2/name/" + countryName)
        .then(response => (this.countrySelectedList = response))
        .then(() => {
          this.countryName = countryName;
        });
    }   
  },
};
</script>

<style scoped>
.ui.sidebar {
  top: 104px;
}
.travelersBackground img {
  padding-top: 20px;
  width: 100%;
}
.ui.page.grid {
  padding-left: 0;
}
.sideBarList {
  margin-top: 50px;
}
.ui.celled.table.column.twelve.wide {
  margin: 30px 60px;
}
.countryTable {
  margin-top: 40px;
}
.ui.table {
  width: 90%;
}
</style>