<template>
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
</template>

<script>
export default {
  name: 'Result',
  props: {
    data: {
      alldata
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
