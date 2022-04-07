<template>
<div>
  <h1>Liste des maisons disponibles</h1>

  <ul id="houses"></ul>
</div>
</template>

<script>
import axios from 'axios';
export default {
data () {
    return {
      info: null,
      loading: true,
      errored: false
    }
  },
  mounted: function(){
    axios({
      url:'http://localhost:1337/api/houses?populate=*',
      method:'GET'
    }).then((response) => {
      var arrayhouse = response.data.data;
      console.log(arrayhouse);

      var list = document.getElementById("houses");

      for(let i = 0; i < arrayhouse.length; i++){
          list.innerHTML += "<li><h3>"+ arrayhouse[i].attributes.Title +"</h3><p>"+ arrayhouse[i].attributes.Price +" €</p>"
          list.innerHTML += "<a href='/fiche?id=" + arrayhouse[i].id + "'>Voir les détails</a></li>"
      }
      
    })
  }
}
</script>