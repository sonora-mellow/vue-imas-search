<template>
    <div class='wrapper'>
        <div class='select_area'>
            <select class='selectJson' v-model='selectJson'>
                    <option value='' selected>select json</option>
                    <option value='all'>all</option>
                    <option value='million'>million</option>
                    <option value='as'>as</option>
                    <option value='shiny'>shiny</option>
            </select>
        </div>
        <div class='search_area'>
            <select class=greeType v-model='searchGreeType'>
                <option value='' selected>greeType</option>
                <option value='Vocal'>Vocal</option>
                <option value='Dance'>Dance</option>
                <option value='Visual'>Visual</option>
            </select>
            <select class=theaterType v-model='searchTheaterType'>
            <option value='' selected>theaterType</option>
            <option value='Princess'>Princess</option>
            <option value='Fairy'>Fairy</option>
            <option value='Angel'>Angel</option>
            </select>
            <select class=bloodType v-model='searchBloodType'>
                <option value='' selected>bloodType</option>
                <option value='A'>A</option>
                <option value='B'>B</option>
                <option value='O'>O</option>
                <option value='AB'>AB</option>
            </select>
            <select class=dominance v-model='searchDominance'>
                <option value='' selected>利き手</option>
                <option value='右利き'>右利き</option>
                <option value='左利き'>左利き</option>
            </select>
        </div>
        <div class='json_area'>
            <div v-if='errored' class='data_box'>
                <p>DataLoad Error</p>
            </div>

            <div v-else>
                <div v-if="loading">Loading...</div>
                {{ axiosdata }}

                <div v-if='filterdata.length == 0' class='data_box'>
                    <p>該当データはありません</p>
                </div>
                <div v-else v-for='idol in filterdata' :key='idol.id'>
                    <IdolList
                        :key='idol.id'
                        :id='idol.id'
                        :greeType='idol.greeType'
                        :theaterType='idol.theaterType'
                        :name='idol.name'
                        :nameRead='idol.nameRead'
                        :acter='idol.acter'
                        :acterRead='idol.acterRead'
                        :imageColor='idol.imageColor'
                        :age='idol.age'
                        :height='idol.height'
                        :weight='idol.weight'
                        :birthPlace='idol.birthPlace'
                        :birthMonth='idol.birthMonth'
                        :birthDay='idol.birthDay'
                        :bloodType='idol.bloodType'
                        :dominance='idol.dominance'
                        :b='idol.b'
                        :w='idol.w'
                        :h='idol.h'
                        :hobby='idol.hobby'
                        :skill='idol.skill'
                        :like='idol.like'
                    ></IdolList>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import IdolList from './IdolList'
const as = require("../assets/json/as.json").as;
const million = require("../assets/json/million.json").million;
const shiny = require("../assets/json/shiny.json").shiny;
const all = million;

const _ = require('lodash');

export default {
  name: 'Search',
  components: {
        IdolList
  },
  data: function() {
    return {
        alldata: null,
        selectJson: '',
        searchGreeType: '',
        searchTheaterType: '',
        searchAge: null,
        searchBloodType: '',
        searchDominance: ''
    }
  },
  mounted() {
    this.alldata = all;
  },
  computed: {
    /* eslint-disable */
    changeJson: function() {
        switch(this.selectJson) {
            case '':
                return this.alldata = all;
            case 'as':
                return this.alldata = as;
            case 'million':
                return this.alldata = million;
            case 'shiny':
                return this.alldata = shiny;
        }
    },
    /* eslint-disable */
    filterGreeType: function() {
        if(!this.searchGreeType == '') {
            return this.alldata.filter(function(el){
                return el.greeType === this.searchGreeType
            }, this);
        } else {
            return this.alldata;
        }
    },
    filterTheaterType: function() {
        if(!this.searchTheaterType == '') {
            return this.alldata.filter(function(el){
                return el.theaterType === this.searchTheaterType
            }, this);
        } else {
            return this.alldata;
        }
    },
    filterAge: function() {
        if(!this.searchAge == null) {
            return this.alldata.filter(function(el){
                return el.age === this.searchAge
            }, this);
        } else {
            return this.alldata;
        }
    },
    filterBloodType: function() {
        if(!this.searchBloodType == '') {
            return this.alldata.filter(function(el){
                return el.bloodType === this.searchBloodType
            }, this);
        } else {
            return this.alldata;
        }
    },
    filterDominance: function() {
        if(!this.searchDominance == '') {
            return this.alldata.filter(function(el){
                return el.dominance === this.searchDominance
            }, this);
        } else {
            return this.alldata;
        }
    },
    filterdata: function() {
        return _.intersection(this.alldata,this.filterGreeType,this.filterTheaterType,this.filterAge,this.filterBloodType,this.filterDominance);
    }
  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@charset "utf-8";
body,p,ul,h1,h2,h3,h4,h5 {
    margin: 0;
    padding: 0;
}
body {
    max-width: 720px;
    margin: 0 auto;
    font-family: 'M PLUS 1p', sans-serif;
}
.select_area {
    margin-top: 20px;
}
.search_area {
    margin-top: 20px;
    margin-bottom: 20px;
}
.select_area select, .search_area select {
    margin-right: 10px;
    padding: 3px 10px;
    border: 1px solid #ccc;
}
</style>