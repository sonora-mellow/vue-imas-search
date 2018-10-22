<template>
    <div class='data_box'>
        <div class='tag_area'>
            <div class='tag gree' :class='greeType'><p>{{ greeType }}</p></div>
            <div class='tag theater' :class='theaterType'><p>{{ theaterType }}</p></div>
        </div>
        <div class='personal_area'>
            <div class='main_area'>
                <div class='icon' :style='{backgroundColor: imageColor}'></div>
                <p><ruby>{{ name }}<rt>{{ nameRead }}</rt></ruby></p>
                <p>CV.<ruby>{{ acter }}<rt>{{ acterRead }}</rt></ruby></p>
            </div>
            <div class='side_area'>
                <p>{{ birthPlace }}出身{{ birthMonth }}/{{ birthDay }}生まれ {{ age }}歳</p>
                <p>{{ bloodType }}型</p>
                <p>{{ dominance }}</p>
                <p>{{ b }}/{{ w }}/{{ w }}</p>
                <dl>
                    <dt>趣味:</dt><dd>{{ hobby }}</dd>
                    <dt>特技:</dt><dd>{{ skill }}</dd>
                    <dt>好きなこと:</dt><dd>{{ like }}</dd>
                </dl>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'IdolList',
  props: {
    id: {
        type: Number,
        default: null
    },
    greeType: {
        type: String,
        default: ''
    },
    theaterType: {
        type: String,
        default: ''
    },
    name: {
        type: String,
        default: ''
    },
    nameRead: {
        type: String,
        default: ''
    },
    acter: {
        type: String,
        default: ''
    },
    acterRead: {
        type: String,
        default: ''
    },
    imageColor: {
        type: String,
        default: ''
    },
    age: {
        type: Number,
        default: null
    },
    height: {
        type: Number,
        default: null
    },
    weight: {
        type: Number,
        default: null
    },
    birthPlace: {
        type: String,
        default: ''
    },
    birthMonth: {
        type: Number,
        default: null
    },
    birthDay: {
        type: Number,
        default: null
    },
    bloodType: {
        type: String,
        default: ''
    },
    dominance: {
        type: String,
        default: ''
    },
    b: {
        type: Number,
        default: null
    },
    w: {
        type: Number,
        default: null
    },
    h: {
        type: Number,
        default: null
    },
    hobby: {
        type: String,
        default: ''
    },
    skill: {
        type: String,
        default: ''
    },
    like: {
        type: String,
        default: ''
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

.Vocal, .Princess {
    background-color: pink;
}
.Dance, .Fairy {
    background-color: cornflowerblue;
}
.Visual, .Angel {
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
