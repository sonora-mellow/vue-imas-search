<template>
  <div class="wrapper">
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
    <div class="json_area">
        <div class='data_box'>
            <div class='tag_area'>
                <div class='tag gree'><p>filterdata[i].greeType</p></div>
                <div class='tag theater'><p>filterdata[i].theaterType</p></div>
            </div>
            <div class='personal_area'>
                <div class='main_area'>
                    <div class='icon'></div>
                    <p><ruby>filterdata[i].name<rt>filterdata[i].nameRead</rt></ruby></p>
                    <p>CV.<ruby>filterdata[i].acter<rt>filterdata[i].acterRead</rt></ruby></p>
                </div>
                <div class='side_area'>
                    <p>filterdata[i].birthPlace出身filterdata[i].birthMonth/filterdata[i].birthDay生まれfilterdata[i].age歳</p>
                    <p>filterdata[i].bloodType型</p>
                    <p>filterdata[i].dominance</p>
                    <p>filterdata[i].b '/'filterdata[i].w'/'filterdata[i].h</p>
                    <dl>
                        <dt>趣味:</dt><dd>filterdata[i].hobby</dd>
                        <dt>特技:</dt><dd>filterdata[i].skill</dd>
                        <dt>好きなこと:</dt><dd>filterdata[i].like</dd>
                    </dl>
                </div>
            </div>
        </div>
    </div>
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
  created: {
    getJSON(){},
    init(data){
        alldata = data;
        filterdata = alldata;
        createAddArea();
        display();
        console.log(filterdata.length);
        console.log(Object.keys(filterdata[0]).length);
        console.log(Object.keys(filterdata[0])[1]);
    },
    display() {
        $json_area.empty();

        if(filterdata.length == 0){
            $(
                "<div class='data_box'>" +
                    "<p>該当データはありません</p>" +
                "</div>"
            )
            .appendTo($json_area);
        } else {
            for(var i=0; i<filterdata.length; i++){
                $(
                    "<div class='data_box'>" +
                        "<div class='tag_area'>" +
                            "<div class='tag gree'><p>" + filterdata[i].greeType + "</p></div>" +
                            "<div class='tag theater'><p>" + filterdata[i].theaterType + "</p></div>" +
                        "</div>" +
                        "<div class='personal_area'>" +
                            "<div class='main_area'>" +
                                "<div class='icon'></div>" +
                                "<p><ruby>" + filterdata[i].name + "<rt>" + filterdata[i].nameRead +  "</rt></ruby></p>" +
                                "<p>" + "CV.<ruby>" + filterdata[i].acter + "<rt>" + filterdata[i].acterRead +  "</rt></ruby></p>" +
                            "</div>" +
                            "<div class='side_area'>" +
                                "<p>" + filterdata[i].birthPlace + "出身　" + filterdata[i].birthMonth + "/" + filterdata[i].birthDay + "生まれ　" + filterdata[i].age + "歳</p>" +
                                "<p>" + filterdata[i].bloodType + "型</p>" +
                                "<p>" + filterdata[i].dominance + "</p>" +
                                "<p>" + filterdata[i].b + '/' + filterdata[i].w + '/' + filterdata[i].h +  "</p>" +
                                "<dl>" +
                                    "<dt>趣味:</dt><dd>" + filterdata[i].hobby + "</dd>" +
                                    "<dt>特技:</dt><dd>" + filterdata[i].skill + "</dd>" +
                                    "<dt>好きなこと:</dt><dd>" + filterdata[i].like + "</dd>" +
                                "</dl>" +
                            "</div>" +
                        "</div>" +
                    "</div>"
                )
                .appendTo($json_area);
            }
            addTagColor();
            addImageColor();
        }
    }
  },
  methods: {
    selectJson() {
        selectjson = $(this).val();
    },
    btnGetJson() {
        switch(selectjson) {
            case 'all':
                console.log(selectjson);
                $.when(
                $.getJSON('./json/million.json'),
                $.getJSON('./json/as.json'),
                $.getJSON('./json/test.json'),
                ).done(function(data_a,data_b,data_c) {
                    console.log(data_a[0]);
                    console.log(data_b[0]);
                    console.log(data_c[0]);
                    data = data_a[0].concat(data_b[0]).concat(data_c[0]);
                    init(data);
                });
                break;
            case 'million':
                console.log(selectjson);
                $.getJSON('./json/million.json',init);
                break;
            case 'as':
                console.log(selectjson);
                $.getJSON('./json/as.json',init);
                break;
            case 'test':
                console.log(selectjson);
                $.getJSON('./json/test.json',init);
                break;
            default:
                break;
        }
    },
    createAddArea(){
        $add_obj_area.empty();
        $(
            "<dl></dl>"
        ).appendTo($add_obj_area);
        for(var i=0; i<Object.keys(alldata[0]).length; i++){
            $(
                "<dt>" +
                Object.keys(alldata[0])[i] + ":</dt>" +
                "<dd><input name='new_" + Object.keys(alldata[0])[i] + "'></dd>"
            )
            .appendTo($('dl'));
        }
        $(
            "<button class='btn_addobj'>add object</button>"
        )
        .appendTo($add_obj_area);
    },
    addTagColor() {
        $('.data_box').each(function(i){
            switch($(this).find('.gree').text()) {
                case 'Vocal':
                    $(this).find('.gree').addClass('vocal');
                    break;
                case 'Dance':
                $(this).find('.gree').addClass('dance');
                    break;
                case 'Visual':
                    $(this).find('.gree').addClass('visual');
                    break;
                default:
                    break;
            }
            switch($(this).find('.theater').text()) {
                case 'Princess':
                    $(this).find('.theater').addClass('princess');
                    break;
                case 'Fairy':
                    $(this).find('.theater').addClass('fairy');
                    break;
                case 'Angel':
                    $(this).find('.theater').addClass('angel');
                    break;
                default:
                    break;
            }
        });
    },
    addImageColor() {
        $('.data_box').each(function(i){
            $(this).find('.icon').css({
                backgroundColor: filterdata[i].imageColor
            })
        });
    },
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
    addObj() {
        const adddata = {};
        console.log(Object.keys(alldata[0]).length);
        for(var i=0; i<Object.keys(alldata[0]).length; i++) {
            num = i;
            adddata[Object.keys(alldata[0])[i]] = $('.add_obj_area p:nth-of-type(' + (num + 1) + ') input').val()
        };
        console.log(adddata);
        alldata.push(adddata);
        filterdata = alldata;
        display();
    },
    addProp() {
        console.log($('.add_prop_area p input').val());
        for(var i=0; i<alldata; i++) {
            alldata[i][$('.add_prop_area p input').val()] = ""
            console.log('test');
        };
        filterdata = alldata;
        console.log(filterdata);
        console.log(Object.keys(alldata[0]).length);
        console.log(alldata[0]);
        display();
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
