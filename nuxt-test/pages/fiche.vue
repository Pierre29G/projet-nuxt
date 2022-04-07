<template>
  <div>
    <h1 id="titre">Fiche</h1>
    <div id="info"></div>
    <a href='/'>Retour à la liste</a>
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
    console.log(this.$route.query.id);
    var urlfiche = 'http://localhost:1337/api/houses/'+this.$route.query.id+'?populate=*';

    axios({
      url:urlfiche,
      method:'GET'
    }).then((response) => {
      var arrayinfo = response.data.data;
      console.log(arrayinfo.attributes);
      console.log(arrayinfo.attributes.Image.data[0].attributes.url);

      document.getElementById("titre").innerHTML = arrayinfo.attributes.Title;

      var info = document.getElementById("info");
      info.innerHTML += "<p>"+ arrayinfo.attributes.Price +" €</p>"
      info.innerHTML += "<p>"+ arrayinfo.attributes.Adresse +"</p><p>"+ arrayinfo.attributes.Desc +"</p>"
      info.innerHTML += "<img src='http://localhost:1337"+ arrayinfo.attributes.Image.data[0].attributes.url +"'>"
      
    })
  }
}
</script>
