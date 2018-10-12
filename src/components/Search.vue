<template>
  <div class="search_area">
    <select class="greeType" @change="changeGreeType()">
        <option value="" selected>greeType</option>
        <option value="all">all</option>
        <option value="Vocal">Vocal</option>
        <option value="Dance">Dance</option>
        <option value="Visual">Visual</option>
    </select>
    <select class="theaterType" @change="changeTheaterType()">
      <option value="" selected>theaterType</option>
      <option value="all">all</option>
      <option value="Princess">Princess</option>
      <option value="Fairy">Fairy</option>
      <option value="Angel">Angel</option>
    </select>
    <input type="number" placeholder="年齢" class="age" @change="changeAge()">
    <select class="bloodType" @change="changeBloodType()">
        <option value="" selected>bloodType</option>
        <option value="all">all</option>
        <option value="A">A</option>
        <option value="B">B</option>
        <option value="O">O</option>
        <option value="AB">AB</option>
      </select>
    <select class="dominance" @change="changeDominance()">
        <option value="" selected>利き手</option>
        <option value="all">all</option>
        <option value="右利き">右利き</option>
        <option value="左利き">左利き</option>
    </select>
    <button class="btn_search" @click="search()">検索</button>
  </div>
</template>
<script>
export default {
  name: 'Search',
  data() {
    return {
      greeType: "",
      theaterType: "",
      name: "",
      nameRead: "",
      acter: "",
      acterRead: "",
      imageColor: "",
      age: "",
      height: "",
      weight: "",
      birthPlace: "",
      birthMonth: "",
      birthDay: "",
      bloodType: "",
      dominance: "",
      b: 88,
      w: 58,
      h: 85,
      hobby: "",
      skill: "",
      like: ""
    }
  },
  methods: {
    changeGreeType() {
      greeType = $(this).val();
    },
    changeTheaterType() {
      theaterType = $(this).val();
    },
    changeAge() {
      age = $(this).val();
    },
    changeBloodType() {
      bloodType = $(this).val();
    },
    ChangeDominance() {
      dominance = $(this).val();
    },
    search() {
      filterdata = [];
      const searching = [];

      searching = $.grep(alldata,function(n){
          if(greeType === undefined || greeType === "" || greeType === "all"){
              return n.greeType !== null
          } else {
              return n.greeType === greeType
          }
      });
      searching = $.grep(searching,function(n){
          if(theaterType === undefined || theaterType === "" || theaterType === "all"){
              return n.theaterType !== null
          } else {
              return n.theaterType === theaterType
          }
      });
      searching = $.grep(searching,function(n){
          if(age === undefined || age === "all"){
              return n.age !== null
          } else {
              return n.age == age
          }
      });
      searching = $.grep(searching,function(n){
          if(bloodType === undefined || bloodType === "" || bloodType === "all"){
              return n.bloodType !== null
          } else {
              return n.bloodType === bloodType
          }
      });
      searching = $.grep(searching,function(n){
          if(dominance === undefined || dominance === "" || dominance === "all"){
              return n.dominance !== null
          } else {
              return n.dominance === dominance
          }
      });

      console.log(greeType);
      console.log(theaterType);
      console.log(age);
      console.log(bloodType);
      console.log(dominance);
      console.log(searching);
      console.log(searching.length);

      filterdata = searching;
      display();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.select_area, .search_area {
    margin-bottom: 20px;
}
</style>
