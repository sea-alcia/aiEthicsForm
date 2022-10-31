<template>
    <v-app id="inspire">
        <v-main class="blue-grey lighten-5">
            <v-container>
                <form>
                    <v-row>
                        <v-col class="mt-2" cols="12">
                            <strong>1. 学年を選択してください</strong>
                        </v-col>
                        <v-select v-model="answer['1-grade']" :items="bachelors" label="学年" class="selectbox">
                        </v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>2. 重要度順に並び替えてください(ドラッグ&ドロップ)</strong>
                        </v-col>
                        <draggable v-model="answer['2-importance']" :options="options" style="padding-left: 2%;"
                            draggable=".item">
                            <span style="font-size: 8px">1位</span>
                            <div class="item" v-for="item in answer['2-importance']" :key="item.id">{{
                                    item.name
                            }}</div>
                            <span style="font-size: 8px">4位</span>
                        </draggable>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>3. 現在の睡眠時間に適切ですか</strong>
                        </v-col>
                        <v-radio-group v-model="answer['3-sleep']" row style="padding-left: 2%;">
                            <v-radio label="過剰" value="過剰"></v-radio>
                            <v-radio label="適切" value="適切"></v-radio>
                            <v-radio label="不足" value="不足"></v-radio>
                        </v-radio-group>
                        <v-col class="mt-2" cols="12">
                            <strong>4. 現在の通勤・通学に適切ですか</strong>
                        </v-col>
                        <v-radio-group v-model="answer['4-commuting']" row style="padding-left: 2%;">
                            <v-radio label="過剰" value="過剰"></v-radio>
                            <v-radio label="適切" value="適切"></v-radio>
                            <v-radio label="不足" value="不足"></v-radio>
                        </v-radio-group>
                        <v-col class="mt-2" cols="12">
                            <strong>5. 現在の労働・勉強に適切ですか</strong>
                        </v-col>
                        <v-radio-group v-model="answer['5-study']" row style="padding-left: 2%;">
                            <v-radio label="過剰" value="過剰"></v-radio>
                            <v-radio label="適切" value="適切"></v-radio>
                            <v-radio label="不足" value="不足"></v-radio>
                        </v-radio-group>
                        <v-col class="mt-2" cols="12">
                            <strong>6. 現在の自由時間に適切ですか</strong>
                        </v-col>
                        <v-radio-group v-model="answer['6-free']" row style="padding-left: 2%;">
                            <v-radio label="過剰" value="過剰"></v-radio>
                            <v-radio label="適切" value="適切"></v-radio>
                            <v-radio label="不足" value="不足"></v-radio>
                        </v-radio-group>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>7. 平日の起床時間を教えてください</strong>
                        </v-col>
                        <v-time-picker v-model="answer['7-weekday']" height="30"
                            :landscape="$vuetify.breakpoint.smAndUp" ampm-in-title color="indigo lighten-1">
                        </v-time-picker>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>8. 休日の起床時間を教えてください</strong>
                        </v-col>
                        <v-time-picker v-model="answer['8-holiday']" :landscape="$vuetify.breakpoint.smAndUp"
                            ampm-in-title color="indigo lighten-1">
                        </v-time-picker>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>9. あなたが住んでいるのは都会？田舎？</strong>
                        </v-col>
                        <v-radio-group v-model="answer['9-urban']" row style="padding-left: 2%;">
                            <v-radio label="都会" value="都会住み"></v-radio>
                            <v-radio label="田舎" value="田舎住み"></v-radio>
                        </v-radio-group>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>10. 何人の友人がいますか(最近連絡を取っている人・ネット含む)</strong>
                        </v-col>
                        <div style="height:90px" />
                        <v-slider v-model="answer['10-friend']" style="padding-left:2%; padding-right: 50%;"
                            thumb-label="always">
                        </v-slider>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>11. 恋人または配偶者がいますか</strong>
                        </v-col>
                        <v-radio-group v-model="answer['11-partner']" row style="padding-left: 2%;">
                            <v-radio label="いる" value="はい"></v-radio>
                            <v-radio label="いない" value="いいえ"></v-radio>
                        </v-radio-group>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>12. 悩みを打ち明けられる人がいますか</strong>
                        </v-col>
                        <v-radio-group v-model="answer['12-problem']" row style="padding-left: 2%;">
                            <v-radio label="いる" value="はい"></v-radio>
                            <v-radio label="いない" value="いいえ"></v-radio>
                        </v-radio-group>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>13. 課題を行うタイミングはいつですか</strong>
                        </v-col>
                        <v-select v-model="answer['13-timing']" :items="timings" label="課題のタイミング" class="selectbox">
                        </v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>14. 1日に平均何食食べますか</strong>
                        </v-col>
                        <div style="height:90px" />
                        <v-slider v-model="answer['14-meal']" max="6" style="padding-left:2%; padding-right: 50%;"
                            thumb-label="always">
                        </v-slider>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>15. 1ヶ月に趣味・娯楽にいくらまで費やせますか</strong>
                        </v-col>
                        <div style="height:120px" />
                        <v-slider v-model="answer['15-amusement']" max="200000" step="10000"
                            style="padding-left:2%; padding-right: 50%;" thumb-label="always" :thumb-size="50">
                        </v-slider>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>16. あなたは実家暮らし？一人暮らし？</strong>
                        </v-col>
                        <v-radio-group v-model="answer['16-living']" row style="padding-left: 2%;">
                            <v-radio label="実家暮らし" value="実家暮らし"></v-radio>
                            <v-radio label="一人暮らし" value="1人暮らし"></v-radio>
                        </v-radio-group>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>17. 今この短期的な瞬間、幸せですか</strong>
                        </v-col>
                        <v-rating v-model="answer['17-short']" background-color="indigo lighten-3" color="indigo" large>
                        </v-rating>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>18. ここ一週間など長期的に見て、幸せですか</strong>
                        </v-col>
                        <v-rating v-model="answer['18-long']" background-color="indigo lighten-3" color="indigo" large>
                        </v-rating>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>19. 朝ごはんは主に何を食べますか</strong>
                        </v-col>
                        <v-select v-model="answer['19-morning']" :items="foods" label="朝ごはん" class="selectbox">
                        </v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>20. 昼ごはんは主に何を食べますか</strong>
                        </v-col>
                        <v-select v-model="answer['20-day']" :items="foods" label="昼ごはん" class="selectbox"></v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>21. 夜ごはんは主に何を食べますか</strong>
                        </v-col>
                        <v-select v-model="answer['21-night']" :items="foods" label="夜ごはん" class="selectbox"></v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>22. カロリーを意識していますか</strong>
                        </v-col>
                        <v-select v-model="answer['22-calorie']" :items="calories" label="カロリー" class="selectbox">
                        </v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>23. 健康に気を使った食事をしていますか</strong>
                        </v-col>
                        <v-select v-model="answer['23-health']" :items="calories" label="健康" class="selectbox">
                        </v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>24. 1食あたりどの程度お金をかけますか</strong>
                        </v-col>
                        <div style="height:90px" />
                        <v-slider v-model="answer['24-expense']" max="10000" step="100"
                            style="padding-left:2%; padding-right: 50%;" thumb-label="always" :thumb-size="40">
                        </v-slider>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>25. 日常的に飲む飲み物はなんですか</strong>
                        </v-col>
                        <v-select v-model="answer['25-everyday']" :items="drinks" label="日常" class="selectbox">
                        </v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>26. 食事中に飲む飲み物はなんですか</strong>
                        </v-col>
                        <v-select v-model="answer['26-eating']" :items="drinks" label="食事中" class="selectbox">
                        </v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>27. 友人との食事の頻度はどれくらいですか</strong>
                        </v-col>
                        <v-select v-model="answer['27-friend']" :items="frequency" label="頻度" class="selectbox">
                        </v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>28. 美味しいものを食べたとき、幸せを感じますか</strong>
                        </v-col>
                        <v-select v-model="answer['28-happy']" :items="happy" label="幸せ" class="selectbox"></v-select>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>29. 人生における食事の重要度はどの程度ですか</strong>
                        </v-col>
                        <v-rating v-model="answer['29-importance']" background-color="indigo lighten-3" color="indigo"
                            large>
                        </v-rating>
                        <div class="newline" />
                        <v-col class="mt-2" cols="12">
                            <strong>30. 現在の食事に満足していますか</strong>
                        </v-col>
                        <v-rating v-model="answer['30-satisfaction']" background-color="indigo lighten-3" color="indigo"
                            large>
                        </v-rating>
                    </v-row>
                    <div class="newline" />
                    <v-btn color="indigo" large class="white--text" @click="onSubmit">
                        送信
                    </v-btn>
                </form>
            </v-container>
        </v-main>
    </v-app>
</template>

<script>
import axios from 'axios'
import draggable from "vuedraggable"

export default {
    components: {
        draggable,
    },
    data: () => ({
        bachelors: ["1年", "2年", "3年", "4年"],
        timings: ["できるタイミングですぐに", "締切日前に適度に", "ギリギリ", "やらない"],
        foods: ["コンビニ飯", "ファストフード店", "飲食店", "居酒屋", "お惣菜", "手作り", "食べない"],
        calories: ["意識している", "できるときに意識している", "あまり意識していない", "意識していない"],
        drinks: ["水", "お茶", "炭酸", "その他清涼飲料水", "お酒"],
        frequency: ["毎日", "週に5~6回", "週に3~4回", "週に1~2回", "月2~3回程度", "月1回未満"],
        happy: ["とても感じる", "感じる", "あまり感じない", "感じない"],

        options: {
            animation: 200
        },
        answer: {
            "1-grade": null,
            "2-importance": [
                { id: 0, name: '睡眠時間' },
                { id: 1, name: '通勤通学時間' },
                { id: 2, name: '労働勉強時間' },
                { id: 3, name: '自由時間' },
            ],
            "3-sleep": null,
            "4-commuting": null,
            "5-study": null,
            "6-free": null,
            "7-weekday": null,
            "8-holiday": null,
            "9-urban": null,
            "10-friend": null,
            "11-partner": null,
            "12-problem": null,
            "13-timing": null,
            "14-meal": null,
            "15-amusement": null,
            "16-living": null,
            "17-short": null,
            "18-long": null,
            "19-morning": null,
            "20-day": null,
            "21-night": null,
            "22-calorie": null,
            "23-health": null,
            "24-expense": null,
            "25-everyday": null,
            "26-eating": null,
            "27-friend": null,
            "28-happy": null,
            "29-importance": null,
            "30-satisfaction": null,
        },
    }),
    methods: {
        onSubmit() {
            let score_p, score_eat; // pが日常, eatが色に関するwell-being

            // score_p, score_eatはそれぞれ21点, 31点満点(大西に文句を言ってくれ)
            score_p = 0;
            score_eat = 0;
            for (let key of Object.keys(this.answer)) {
                // 都会(1点) or 田舎(2点)
                if (key == '9-urban') {
                    if (this.answer[key] == '都会住み') {
                        score_p += 1;
                    }
                    else {
                        score_p += 2;
                    }
                }

                // 恋人いる(1点)
                if (key == '11-partner' & this.answer[key] == 'はい') {
                    score_p += 1;
                } 

                // 困った時に相談相手がいる(1点)
                if (key == '12-problem' & this.answer[key] == 'はい') {
                    score_p += 1;
                } 

                // 課題のやるタイミングがすぐ(4点) or ギリギリ(2点) or 締切日前に適度に(1点)
                if (key == '13-timing') {
                    if (this.answer[key] == '出来るタイミングですぐに') {
                        score_p += 4;
                    }
                    else if (this.answer[key] == 'ギリギリ') {
                        score_p += 2;
                    }
                    else if (this.answer[key] == '締切日前に適度に') {
                        score_p += 1;
                    }
                }

                // どれだけ趣味にお金を使うかが15000以下(1点) or 5万まで(2点) or 10万まで(3点)
                if (key == '15-amusement') {
                    if (this.answer[key] <= 15000) {
                        score_p += 1;
                    }
                    else if (this.answer[key] > 15000 & this.answer[key] <= 50000) {
                        score_p += 2;
                    }
                    else if (this.answer[key] > 50000 & this.answer[key] <= 100000) {
                        score_p += 3;
                    }
                }

                // 一人暮らし(1点)
                if (key == '16-living' & this.answer[key] == '1人暮らし') {
                    score_p += 1;
                }

                // 労働の重要度の低さ(低いほど得点)
                // 自由度が4位以外(1点)
                if (key == '2-importance') {
                    for (var data of this.answer[key]) {
                        if (data['name'] == '労働勉強時間') {
                            score_p += data['id'];
                        }
                        if (data['id'] == 3 & data['name'] != '自由時間') {
                            score_p += 1;
                        }
                    }
                }

                // 睡眠時間が過剰(1点)
                if (key == '3-sleep' & this.answer[key] == '過剰') {
                    score_p += 1;
                }

                // 通勤時間が過剰(1点) or 適切(2点)
                if (key == '4-commuting') {
                    if (this.answer[key] == '過剰') {
                        score_p += 1;
                    }
                    else if (this.answer[key] == '適切') {
                        score_p += 2;
                    }
                }

                // 労働時間が不足(1点) or 適切(2点)
                if (key == '5-study') {
                    if (this.answer[key] == '不足') {
                        score_p += 1;
                    }
                    else if (this.answer[key] == '適切') {
                        score_p += 2;
                    }
                }

                // 食事回数が3~4回(2点)
                if (key == '14-meal' & this.answer[key] >= 3 & this.answer[key] <= 4) {
                    score_eat += 2;
                }

                // 朝ご飯がコンビニ(3点) or 手作り(2点)
                if (key == '19-morning') {
                    if (this.answer[key] == 'コンビニ飯') {
                        score_eat += 3;
                    }
                    if (this.answer[key] == '手作り') {
                        score_eat += 2;
                    }
                }

                // お昼ご飯(省略)
                if (key == '20-day') {
                    if (this.answer[key] == 'コンビニ飯' || this.answer[key] == '手作り') {
                        score_eat += 3;
                    }
                    else if (this.answer[key] == 'お惣菜' || this.answer[key] == 'ファストフード店') {
                        score_eat += 5;
                    }
                    else if (this.answer[key] == '飲食店') {
                        score_eat += 2;
                    }
                }

                // 夜ご飯(省略)
                if (key == '21-night') {
                    if (this.answer[key] == '飲食店' || this.answer[key] == '手作り') {
                        score_eat += 2;
                    }
                    else if (this.answer[key] == 'コンビニ飯') {
                        score_eat += 1;
                    }
                    else if (this.answer[key] == 'お惣菜') {
                        score_eat += 4;
                    }
                    else if (this.answer[key] == '居酒屋') {
                        score_eat += 3;
                    }
                }

                // カロリー意識
                if (key == '22-calorie') {
                    if (this.answer[key] == 'あまり意識していない') {
                        score_eat += 1;
                    }
                    else if (this.answer[key] == '意識している') {
                        score_eat += 2;
                    }
                }

                // 健康
                if (key == '23-health') {
                    if (this.answer[key] == '意識していない') {
                        score_eat += 3;
                    }
                    else if (this.answer[key] == 'できるときに意識している') {
                        score_eat += 2;
                    }
                    else if (this.answer[key] == '意識している') {
                        score_eat += 1;
                    }
                }

                // 日常での飲み物
                if (key == '25-everyday') {
                    if (this.answer[key] == 'お茶') {
                        score_eat += 3;
                    }
                    else if (this.answer[key] == '水') {
                        score_eat += 2;
                    }
                    else if (this.answer[key] == 'その他清涼飲料水' || this.answer[key] == '炭酸') {
                        score_eat += 1;
                    }
                }

                // 食事での飲み物
                if (key == '26-eating') {
                    if (this.answer[key] == 'お茶') {
                        score_eat += 1;
                    }
                    else if (this.answer[key] == '水') {
                        score_eat += 2;
                    }
                }

                // 食での幸せ
                if (key == '28-happy') {
                    if (this.answer[key] == 'あまり感じない') {
                        score_eat += 1;
                    }
                    else if (this.answer[key] == 'とても感じる' || this.answer[key] == '感じる') {
                        score_eat += 2;
                    }
                }

                // 食の重要度
                if (key == '29-importance') {
                    if (this.answer[key] == 1) {
                        score_eat += 3;
                    }
                    else if (this.answer[key] == 2) {
                        score_eat += 2;
                    }
                }

                // 食の満足度
                if (key == '30-satisfaction') {
                    if (this.answer[key] == 2) {
                        score_eat += 1;
                    }
                    else if (this.answer[key] >= 3) {
                        score_eat += 2;
                    }
                }
            }

            console.log(score_p)
            console.log(score_eat)
            alart(score_p, score_eat);
        }
    }
}
</script>

<style>
.selectbox {
    padding-left: 2%;
    padding-right: 70%;
}

.newline {
    height: 50px;
}

.item {
    display: inline-block;
    font-size: 12px;
    margin: 5px;
    padding: 8px;
    border-radius: 12px;
    color: #eeeeee;
    background-color: #5C6BC0;
}

.item:hover {
    cursor: grab;
}

.item:active {
    cursor: grabbing;
}
</style>
