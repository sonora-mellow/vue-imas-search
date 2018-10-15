<template>
    <div class="wrapper">
        <div class="add_area">
            <div class="add_obj_area">
                <dl></dl>
            </div>
            <div class="add_prop_area">
                <p>newProp: <input name="new_prop"></p>
                <button class='btn_addprop'>add prop</button>
            </div>
        </div>
        <div class="select_area">
            <select class="select_json" v-model="selectJson">
                    <option value="" selected>select json</option>
                    <option value="all">all</option>
                    <option value="million">million</option>
                    <option value="as">as</option>
                    <option value="test">test</option>
            </select>
            <button class="btn_getjson">get json</button>
        </div>
        <div class="search_area">
            <select class=greeType v-model="searchGreeType">
                <option value="" selected>greeType</option>
                <option value="all">all</option>
                <option value="Vocal">Vocal</option>
                <option value="Dance">Dance</option>
                <option value="Visual">Visual</option>
            </select>
            <select class=theaterType v-model="searchTheaterType">
            <option value="" selected>theaterType</option>
            <option value="all">all</option>
            <option value="Princess">Princess</option>
            <option value="Fairy">Fairy</option>
            <option value="Angel">Angel</option>
            </select>
            <input type="number" placeholder="年齢" class=age v-model="searchAge">
            <select class=bloodType v-model="searchBloodType">
                <option value="" selected>bloodType</option>
                <option value="all">all</option>
                <option value="A">A</option>
                <option value="B">B</option>
                <option value="O">O</option>
                <option value="AB">AB</option>
            </select>
            <select class=dominance v-model="searchDominance">
                <option value="" selected>利き手</option>
                <option value="all">all</option>
                <option value="右利き">右利き</option>
                <option value="左利き">左利き</option>
            </select>
            <button class="btn_search" @click="search()">検索</button>
        </div>
        <div class="json_area">
            <div class='data_box' v-for="idol in alldata" :key="idol.id">
                <div class='tag_area'>
                    <div class='tag gree'><p>{{ idol.greeType }}</p></div>
                    <div class='tag theater'><p>{{ idol.theaterType }}</p></div>
                </div>
                <div class='personal_area'>
                    <div class='main_area'>
                        <div class='icon'></div>
                        <p><ruby>{{ idol.name }}<rt>{{ idol.nameRead }}</rt></ruby></p>
                        <p>CV.<ruby>{{ idol.acter }}<rt>{{ idol.acterRead }}</rt></ruby></p>
                    </div>
                    <div class='side_area'>
                        <p>{{ idol.birthPlace }}出身{{ idol.birthMonth }}/{{ idol.birthDay }}生まれ {{ idol.age }}歳</p>
                        <p>{{ idol.bloodType }}型</p>
                        <p>{{ idol.dominance }}</p>
                        <p>{{ idol.b }}/{{ idol.w }}/{{ idol.w }}</p>
                        <dl>
                            <dt>趣味:</dt><dd>{{ idol.hobby }}</dd>
                            <dt>特技:</dt><dd>{{ idol.skill }}</dd>
                            <dt>好きなこと:</dt><dd>{{ idol.like }}</dd>
                        </dl>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
// import idols from '../json/'

export default {
  name: 'Search',
//   mixins: [ idols ],
  data() {
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
        filterdata: [],
        selectJson: '',
        searchGreeType: '',
        searchTheaterType: '',
        searchAge: '',
        searchBloodType: '',
        searchDominance: ''
    }
  },
  created: {
    // getJSON(){
    //     const req = new XMLHttpRequest();		  // XMLHttpRequestオブジェクトを生成する
    //     req.onreadystatechange = function() {		  // XMLHttpRequestオブジェクトの状態が変化した際に呼び出されるイベントハンドラ
    //         if(req.readyState == 4 && req.status == 200){ // サーバーからのレスポンスが完了し、かつ、通信が正常に終了した場合
    //         alert(req.responseText);		          // 取得した JSON ファイルの中身を表示
    //         }
    //     };
    //     req.open("GET", "million.json", false); // HTTPメソッドとアクセスするサーバーのURLを指定
    //     req.send(null);					    // 実際にサーバーへリクエストを送信
    // },
    init: function(){
        // alldata = data;
        this.filterdata = this.alldata
        // createAddArea();
        // display();
        // console.log(filterdata.length);
        // console.log(Object.keys(filterdata[0]).length);
        // console.log(Object.keys(filterdata[0])[1]);
    },
    display: function(){
        // $json_area.empty();
        // const json_area = document.getElementById('json_area');
        // const alldata = alldata;
        // const filterdata = alldata;

        // json_area.innerHTML += this.msg

        // if(filterdata.length == 0){
        //       json_area.innerHTML += 
        //         "<div class='data_box'>" +
        //             "<p>該当データはありません</p>" +
        //         "</div>"
        // } else {
        //     for(let i=0; i<filterdata.length; i++){
        //         json_area.innerHTML += 
        //         "<div class='data_box'>" +
        //             "<div class='tag_area'>" +
        //                 "<div class='tag gree'><p>" + filterdata[i].greeType + "</p></div>" +
        //                 "<div class='tag theater'><p>" + filterdata[i].theaterType + "</p></div>" +
        //             "</div>" +
        //             "<div class='personal_area'>" +
        //                 "<div class='main_area'>" +
        //                     "<div class='icon'></div>" +
        //                     "<p><ruby>" + filterdata[i].name + "<rt>" + filterdata[i].nameRead +  "</rt></ruby></p>" +
        //                     "<p>" + "CV.<ruby>" + filterdata[i].acter + "<rt>" + filterdata[i].acterRead +  "</rt></ruby></p>" +
        //                 "</div>" +
        //                 "<div class='side_area'>" +
        //                     "<p>" + filterdata[i].birthPlace + "出身" + filterdata[i].birthMonth + "/" + filterdata[i].birthDay + "生まれ" + filterdata[i].age + "歳</p>" +
        //                     "<p>" + filterdata[i].bloodType + "型</p>" +
        //                     "<p>" + filterdata[i].dominance + "</p>" +
        //                     "<p>" + filterdata[i].b + '/' + filterdata[i].w + '/' + filterdata[i].h +  "</p>" +
        //                     "<dl>" +
        //                         "<dt>趣味:</dt><dd>" + filterdata[i].hobby + "</dd>" +
        //                         "<dt>特技:</dt><dd>" + filterdata[i].skill + "</dd>" +
        //                         "<dt>好きなこと:</dt><dd>" + filterdata[i].like + "</dd>" +
        //                     "</dl>" +
        //                 "</div>" +
        //             "</div>" +
        //         "</div>";
        //     }
        //     this.addTagColor();
        //     this.addImageColor();
        // }
    },
    addTagColor: function() {
        document.querySelectorAll('data_box').each(function(){
            switch(document.querySelector('gree').textContent) {
                case 'Vocal':
                    document.querySelector('gree').classList.add('vocal');
                    break;
                case 'Dance':
                this.querySelector('gree').classList.add('dance');
                    break;
                case 'Visual':
                    this.querySelector('gree').classList.add('visual');
                    break;
                default:
                    break;
            }
            switch(document.querySelectorAll('theater').textContent) {
                case 'Princess':
                    this.querySelectorAll('theater').classList.add('princess');
                    break;
                case 'Fairy':
                    this.querySelectorAll('theater').classList.add('fairy');
                    break;
                case 'Angel':
                    this.querySelectorAll('theater').classList.add('angel');
                    break;
                default:
                    break;
            }
        });
    },
    addImageColor: function() {
        document.querySelectorAll('data_box').each(function(){
            document.querySelectorAll('icon').setAttribute(
                'backgroundColor', this.imageColor
            )
        });
    }
  },
  methods: {
    // changeGreeType: function() {
    //   this.greeType = this.value;
    // },
    // changeTheaterType: function() {
    //   this.theaterType = this.value;
    // },
    // changeAge: function() {
    //   this.age = this.value;
    // },
    // changeBloodType: function() {
    //   this.bloodType = this.value;
    // },
    // ChangeDominance: function() {
    //   this.dominance = this.value;
    // },
    search: function() {
      const alldata = [];
      const searching = [];

      this.searching = alldata.filter(function(n) {
          if(this.greeType === undefined || this.greeType === "" || this.greeType === "all"){
              return n.greeType !== null
          } else {
              return n.greeType === this.greeType
          }
      });
      this.searching = searching.filter(function(n) {
          if(this.theaterType === undefined || this.theaterType === "" || this.theaterType === "all"){
              return n.theaterType !== null
          } else {
              return n.theaterType === this.theaterType
          }
      });
      this.searching = searching.filter(function(n) {
          if(this.age === undefined || this.age === "all"){
              return n.age !== null
          } else {
              return n.age == this.age
          }
      });
      this.searching = searching.filter(function(n) {
          if(this.bloodType === undefined || this.bloodType === "" || this.bloodType === "all"){
              return n.bloodType !== null
          } else {
              return n.bloodType === this.bloodType
          }
      });
      this.searching = searching.filter(function(n) {
          if(this.dominance === undefined || this.dominance === "" || this.dominance === "all"){
              return n.dominance !== null
          } else {
              return n.dominance === this.dominance
          }
      });

    //   console.log(greeType);
    //   console.log(theaterType);
    //   console.log(age);
    //   console.log(bloodType);
    //   console.log(dominance);
    //   console.log(searching);
    //   console.log(searching.length);

      this.filterdata = searching;
      this.display();
    }
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

.select_area, .search_area {
    margin-bottom: 20px;
}

.data_box {
    width: 100%;
    margin: 0 auto 20px;
}

.tag {
    display: inline-block;
    padding: 5px 10px;
    margin-right: 2px;
    border-radius: 10px 10px 0 0 / 10px 10px 0 0;
    border-top: 1px solid #ccc;
    border-left: 1px solid #ccc;
    border-right: 1px solid #ccc;
}

.vocal, .princess {
    background-color: pink;
}
.dance, .fairy {
    background-color: cornflowerblue;
}
.visual, .angel {
    background-color: yellow;
}

.add_obj_area dl {
    margin: 0;
}
.add_obj_area dt {
    display: inline-block;
    width: 20%;
    text-align: right;
}
.add_obj_area dd {
    display: inline-block;
    width: calc(80% - 10px);
    margin-left: 10px;
}

.personal_area {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding: 10px;
    box-sizing: border-box;
    border: 1px solid #ccc;
}

.main_area {
    width: 200px;
    height: 200px;
    padding: 10px;
    box-sizing: border-box;
    text-align: center;
    border: 1px dotted #ccc;
}

.main_area p:nth-of-type(1) {
    margin-bottom: 3px;
}
.main_area p:nth-of-type(2) {
    font-size: 0.8em;
    color: #888;
}

.icon {
    width: 100px;
    height: 100px;
    margin: 0 auto 10px;
    border-radius: 50%;
    background-color: pink;
}

.side_area {
    width: calc(100% - (200px + 10px));
    padding: 10px;
    box-sizing: border-box;
    border: 1px dotted #ccc;
}

.side_area dl {
    margin: 0;
}

.side_area dt {
    display: inline-block;
    width: 20%;
    text-align: right;
}
.side_area dd {
    display: inline-block;
    width: calc(80% - 10px);
    margin-left: 10px;
}
</style>
