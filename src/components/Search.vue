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
</template>
<script>
import IdolList from './IdolList'
import axios from 'axios'

const _ = require('lodash');

export default {
  name: 'Search',
  components: {
        IdolList
  },
  data: function() {
    return {
        alldata: [
            {
                id: 1,
                greeType: "Vocal",
                theaterType: "Princess",
                name: "天海 春香",
                nameRead: "あまみ はるか",
                acter: "中村 繪里子",
                acterRead: "なかむら えりこ",
                imageColor: "#e22b30",
                age: 17,
                height: 158,
                weight: 46,
                birthPlace: "神奈川県",
                birthMonth: 4,
                birthDay: 3,
                bloodType: "O",
                dominance: "右利き",
                b: 83,
                w: 56,
                h: 82,
                hobby: "カラオケ、長電話",
                skill: "お菓子作り",
                like: "歌うこと"
            },
            {
                id: 2,
                greeType: "Vocal",
                theaterType: "Fairy",
                name: "如月 千早",
                nameRead: "きさらぎ ちはや",
                acter: "今井 麻美",
                acterRead: "いまい あさみ",
                imageColor: "#2743d2",
                age: 16,
                height: 162,
                weight: 41,
                birthPlace: "東京都",
                birthMonth: 2,
                birthDay: 25,
                bloodType: "A",
                dominance: "右利き",
                b: 72,
                w: 55,
                h: 78,
                hobby: "音楽鑑賞",
                skill: "歌",
                like: "トレーニング"
            },
            {
                id: 3,
                greeType: "Vocal",
                theaterType: "Fairy",
                name: "四条 貴音",
                nameRead: "しじょう たかね",
                acter: "原 由実",
                acterRead: "はら ゆみ",
                imageColor: "#a6126a",
                age: 18,
                height: 169,
                weight: 49,
                birthPlace: "京都府？",
                birthMonth: 1,
                birthDay: 21,
                bloodType: "B",
                dominance: "右利き",
                b: 90,
                w: 62,
                h: 92,
                hobby: "天体観測、歴史",
                skill: "直感",
                like: "ラーメン"
            },
            {
                id: 4,
                greeType: "Vocal",
                theaterType: "Angel",
                name: "三浦 あずさ",
                nameRead: "みうら あずさ",
                acter: "たかはし 智秋",
                acterRead: "たかはし ちあき",
                imageColor: "#9238be",
                age: 21,
                height: 168,
                weight: 48,
                birthPlace: "千葉県",
                birthMonth: 7,
                birthDay: 19,
                bloodType: "O",
                dominance: "右利き",
                b: 91,
                w: 59,
                h: 86,
                hobby: "犬の散歩",
                skill: "占い",
                like: "カフェ巡り"
            },
            {
                id: 5,
                greeType: "Vocal",
                theaterType: "Fairy",
                name: "水瀬 伊織",
                nameRead: "みなせ いおり",
                acter: "釘宮 理恵",
                acterRead: "くぎみや りえ",
                imageColor: "#fd99e1",
                age: 15,
                height: 153,
                weight: 40,
                birthPlace: "東京都",
                birthMonth: 5,
                birthDay: 5,
                bloodType: "AB",
                dominance: "右利き",
                b: 77,
                w: 54,
                h: 79,
                hobby: "海外旅行、食べ歩き",
                skill: "ショッピング",
                like: "果汁100%オレンジジュース"
            },
            {
                id: 6,
                greeType: "Dance",
                theaterType: "Princess",
                name: "我那覇 響",
                nameRead: "がなは ひびき",
                acter: "沼倉 愛美",
                acterRead: "ぬまくら まなみ",
                imageColor: "#01adb9",
                age: 16,
                height: 152,
                weight: 41,
                birthPlace: "沖縄県",
                birthMonth: 10,
                birthDay: 10,
                bloodType: "A",
                dominance: "右利き",
                b: 83,
                w: 56,
                h: 80,
                hobby: "編み物、卓球",
                skill: "家事全般",
                like: "散歩、動物"
            },
            {
                id: 7,
                greeType: "Dance",
                theaterType: "Princess",
                name: "菊池 真",
                nameRead: "きくち まこと",
                acter: "平田 宏美",
                acterRead: "ひらた ひろみ",
                imageColor: "#515558",
                age: 17,
                height: 159,
                weight: 44,
                birthPlace: "静岡県",
                birthMonth: 8,
                birthDay: 29,
                bloodType: "O",
                dominance: "右利き",
                b: 75,
                w: 57,
                h: 78,
                hobby: "スポーツ全般",
                skill: "空手、ダンス",
                like: "ぬいぐるみ"
            },
            {
                id: 8,
                greeType: "Dance",
                theaterType: "Angel",
                name: "高槻 やよい",
                nameRead: "たかつき やよい",
                acter: "仁後 真耶子",
                acterRead: "にご まやこ",
                imageColor: "#f39939",
                age: 14,
                height: 145,
                weight: 37,
                birthPlace: "埼玉県",
                birthMonth: 3,
                birthDay: 25,
                bloodType: "O",
                dominance: "右利き",
                b: 74,
                w: 54,
                h: 78,
                hobby: "オセロ、野球",
                skill: "節約、家庭菜園",
                like: "家族"
            },
            {
                id: 9,
                greeType: "Visual",
                theaterType: "Fairy",
                name: "秋月 律子",
                nameRead: "あきづき りつこ",
                acter: "若林 直美",
                acterRead: "わかばやし なおみ",
                imageColor: "#01a860",
                age: 19,
                height: 156,
                weight: 43,
                birthPlace: "東京都",
                birthMonth: 6,
                birthDay: 23,
                bloodType: "A",
                dominance: "右利き",
                b: 85,
                w: 57,
                h: 85,
                hobby: "資格取得",
                skill: "分析・実践",
                like: "ゲーム、小説"
            },
            {
                id: 10,
                greeType: "Visual",
                theaterType: "Princess",
                name: "萩原 雪歩",
                nameRead: "はぎわら ゆきほ",
                acter: "浅倉 杏美",
                acterRead: "あさくら あずみ",
                imageColor: "#d3dde9",
                age: 17,
                height: 155,
                weight: 42,
                birthPlace: "東京都",
                birthMonth: 12,
                birthDay: 24,
                bloodType: "A",
                dominance: "右利き",
                b: 81,
                w: 56,
                h: 81,
                hobby: "MY詩集を書くこと",
                skill: "日本茶をいれること",
                like: "ブログ"
            },
            {
                id: 11,
                greeType: "Visual",
                theaterType: "Angel",
                name: "双海 亜美",
                nameRead: "ふたみ あみ",
                acter: "下田 麻美",
                acterRead: "しもだ あさみ",
                imageColor: "#ffe43f",
                age: 13,
                height: 158,
                weight: 42,
                birthPlace: "東京都",
                birthMonth: 5,
                birthDay: 22,
                bloodType: "B",
                dominance: "右利き",
                b: 78,
                w: 55,
                h: 77,
                hobby: "メール、エコ",
                skill: "モノマネ",
                like: "遊ぶこと"
            },
            {
                id: 12,
                greeType: "Visual",
                theaterType: "Angel",
                name: "双海 真美",
                nameRead: "ふたみ まみ",
                acter: "下田 麻美",
                acterRead: "しもだ あさみ",
                imageColor: "#ffe43f",
                age: 13,
                height: 158,
                weight: 42,
                birthPlace: "東京都",
                birthMonth: 5,
                birthDay: 22,
                bloodType: "B",
                dominance: "左利き",
                b: 78,
                w: 55,
                h: 77,
                hobby: "メール、ゲーム",
                skill: "モノマネ",
                like: "遊ぶこと"
            },
            {
                id: 13,
                greeType: "Visual",
                theaterType: "Angel",
                name: "星井 美希",
                nameRead: "ほしい みき",
                acter: "長谷川 明子",
                acterRead: "はせがわ あきこ",
                imageColor: "#b4e04b",
                age: 15,
                height: 161,
                weight: 45,
                birthPlace: "神奈川県",
                birthMonth: 11,
                birthDay: 23,
                bloodType: "B",
                dominance: "右利き",
                b: 86,
                w: 55,
                h: 83,
                hobby: "友達とおしゃべり、ネイルアート",
                skill: "寝ること",
                like: "おにぎり、いちごババロア"
            }
        ],
        jsondata: [],
        errors: [],
        selectJson: '',
        searchGreeType: '',
        searchTheaterType: '',
        searchAge: null,
        searchBloodType: '',
        searchDominance: ''
    }
  },
  beforeCreate: {
    init: function() {
      axios.get("../json/million.json")
        .then(response => {
            this.jsondata.push(response.data);
            //console.log(response);
        })
        .catch(error => {
            this.errors.push(error);
            //console.log(error);
        });
    }
  },
  computed: {
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