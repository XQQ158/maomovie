<template>
    <div v-if="seatData" class="seats-page">
        <div class="info-block underline">
            <div class="movie-name">{{seatData.movie.movieName}}</div>
            <div class="show-info">
                <span class="date">{{seatData.show.showDate}}</span>
                <span class="time">{{seatData.show.showTime}}</span>
                <span class="lang">{{seatData.show.lang}}{{seatData.show.dim}}</span>
            </div>
        </div>
        <div class="select-block">
            <div class="title">
                {{seatData.hall.hallName}}
            </div>
            <div class="seats-block">
                <div class="sideBar-num">
                    <div class="num" v-for="(item,index) in seats" :key="index">
                        {{item.rowId}}
                    </div>
                </div>
                <div class="seats-row" v-for="(row,index) in seats" :key="index">
                    <div class="seats-col" :class="seat.seatType" @click="selectSeat(index,row.rowId,i,seat.seatType,seat.seatNo)" v-for="(seat,i) in row.seats" :key="i"></div>
                    <!-- <div class="seats-col" :class="seat.st" @click="selectSeat(index,row.rowId,i,seat.st,seat.seatNo)" v-for="(seat,i) in row.columns" :key="i"></div> -->
                </div>
            </div>
        </div>
        <div class="buy-block">
            <div class="seat-info">
                <span class="seat-type choose">可选</span>
                <span class="seat-type selected">已选</span>
                <span class="seat-type sold">已售</span>
                <span class="seat-type lover">情侣座</span>
            </div>
            <!-- <div v-if="!selectedArr.length && seatData.seat.bestRecommendation" class="recommend-price-block">
                <span class="title">推荐座位</span>
                <span @click="chooseBestRecommend(index,item)" class="recommend" v-for="(item,index) in bestRecommendation" :key="index">{{index+1}}人</span>
            </div> -->
            <div v-if="selectedArr.length" class="selected-price-block">
            <!-- <div v-else class="selected-price-block"> -->
                <p class="title">已选座位</p>
                <div class="selected">
                    <div class="selected-item" v-for="(item,index) in selectedArr" :key="index">
                        <span class="position">{{item.position}}</span>
                        <span class="price">￥{{price}}</span>
                        <span @click="deleteSelect(index)" class="delete">x</span>
                    </div>
                </div>
            </div>
            <div class="submit-block">
                <mt-button @click="isLogin" type="danger" size="large" :disabled="showBtn">{{btnText}}</mt-button>
            </div>
        </div>
    </div>
</template>

<script>
const SELECT = 'S';    //已选座位 绿
const NOT_SELECT = 'N';//未选座位 白
const EMPTY = 'E';     //空座位
const LK = 'LK'        //不能选择的座位 红

export default {
    name:'seats-page',
    inject:['app'],
    data () {
        return {
            btnText:'请先选座',
            price:this.$route.query.p,
            // seatData:null,
            seatData:{
                "cinema": {
                    "cinemaId": 16840,
                    "cinemaName": "上影青浦时光国际影城"
                },
                "hall": {
                    "hallId": 94424,
                    "hallName": "杜比全景声60帧激光巨幕厅"
                },
                "movie": {
                    "movieId": 1203734,
                    "movieName": "多力特的奇幻冒险"
                },
                "show": {
                    "dim": "3D",
                    "lang": "英语",
                    "showDate": "2020-07-29",
                    "showTime": "12:50",
                    
                },
            },
            seats:[
                {
                    "rowId": "1",
                    "rowNum": 1,
                    "seats": [
                        {
                            "columnId": "23",
                            "rowId": "1",
                            "seatNo": "24",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "22",
                            "rowId": "1",
                            "seatNo": "25",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "1",
                            "seatNo": "26",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "1",
                            "seatNo": "27",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "1",
                            "seatNo": "28",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "1",
                            "seatNo": "29",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "1",
                            "seatNo": "30",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "1",
                            "seatNo": "31",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "1",
                            "seatNo": "32",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "1",
                            "seatNo": "33",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "1",
                            "seatNo": "34",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "1",
                            "seatNo": "35",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "1",
                            "seatNo": "36",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "1",
                            "seatNo": "37",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "1",
                            "seatNo": "38",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "1",
                            "seatNo": "39",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "1",
                            "seatNo": "40",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "1",
                            "seatNo": "41",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "1",
                            "seatNo": "42",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "1",
                            "seatNo": "43",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "1",
                            "seatNo": "44",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "1",
                            "seatNo": "45",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "1",
                            "seatNo": "46",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "2",
                    "rowNum": 2,
                    "seats": [
                        {
                            "columnId": "23",
                            "rowId": "2",
                            "seatNo": "47",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "22",
                            "rowId": "2",
                            "seatNo": "48",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "2",
                            "seatNo": "49",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "2",
                            "seatNo": "50",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "2",
                            "seatNo": "51",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "2",
                            "seatNo": "52",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "2",
                            "seatNo": "53",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "2",
                            "seatNo": "54",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "2",
                            "seatNo": "55",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "2",
                            "seatNo": "56",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "2",
                            "seatNo": "57",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "2",
                            "seatNo": "58",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "2",
                            "seatNo": "59",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "2",
                            "seatNo": "60",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "2",
                            "seatNo": "61",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "2",
                            "seatNo": "62",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "2",
                            "seatNo": "63",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "2",
                            "seatNo": "64",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "2",
                            "seatNo": "65",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "2",
                            "seatNo": "66",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "2",
                            "seatNo": "67",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "2",
                            "seatNo": "68",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "2",
                            "seatNo": "69",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "3",
                    "rowNum": 3,
                    "seats": [
                        {
                            "columnId": "23",
                            "rowId": "3",
                            "seatNo": "70",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "22",
                            "rowId": "3",
                            "seatNo": "71",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "3",
                            "seatNo": "72",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "3",
                            "seatNo": "73",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "3",
                            "seatNo": "74",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "3",
                            "seatNo": "75",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "3",
                            "seatNo": "76",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "3",
                            "seatNo": "77",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "3",
                            "seatNo": "78",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "3",
                            "seatNo": "79",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "3",
                            "seatNo": "80",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "3",
                            "seatNo": "81",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "3",
                            "seatNo": "82",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "3",
                            "seatNo": "83",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "3",
                            "seatNo": "84",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "3",
                            "seatNo": "85",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "3",
                            "seatNo": "86",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "3",
                            "seatNo": "87",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "3",
                            "seatNo": "88",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "3",
                            "seatNo": "89",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "3",
                            "seatNo": "90",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "3",
                            "seatNo": "91",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "3",
                            "seatNo": "92",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "4",
                    "rowNum": 4,
                    "seats": [
                        {
                            "columnId": "23",
                            "rowId": "4",
                            "seatNo": "93",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "22",
                            "rowId": "4",
                            "seatNo": "94",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "4",
                            "seatNo": "95",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "4",
                            "seatNo": "96",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "4",
                            "seatNo": "97",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "4",
                            "seatNo": "98",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "4",
                            "seatNo": "99",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "4",
                            "seatNo": "100",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "4",
                            "seatNo": "101",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "4",
                            "seatNo": "102",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "4",
                            "seatNo": "103",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "4",
                            "seatNo": "104",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "4",
                            "seatNo": "105",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "4",
                            "seatNo": "106",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "4",
                            "seatNo": "107",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "4",
                            "seatNo": "108",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "4",
                            "seatNo": "109",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "4",
                            "seatNo": "110",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "4",
                            "seatNo": "111",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "4",
                            "seatNo": "112",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "4",
                            "seatNo": "113",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "4",
                            "seatNo": "114",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "4",
                            "seatNo": "115",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "5",
                    "rowNum": 5,
                    "seats": [
                        {
                            "columnId": "",
                            "rowId": "5",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "5",
                            "seatNo": "117",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "5",
                            "seatNo": "118",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "5",
                            "seatNo": "119",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "5",
                            "seatNo": "120",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "5",
                            "seatNo": "121",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "5",
                            "seatNo": "122",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "5",
                            "seatNo": "123",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "5",
                            "seatNo": "124",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "5",
                            "seatNo": "125",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "5",
                            "seatNo": "126",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "5",
                            "seatNo": "127",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "5",
                            "seatNo": "128",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "5",
                            "seatNo": "129",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "5",
                            "seatNo": "130",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "5",
                            "seatNo": "131",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "5",
                            "seatNo": "132",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "5",
                            "seatNo": "133",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "5",
                            "seatNo": "134",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "5",
                            "seatNo": "135",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "5",
                            "seatNo": "136",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "5",
                            "seatNo": "137",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "",
                            "rowId": "5",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "6",
                    "rowNum": 6,
                    "seats": [
                        {
                            "columnId": "",
                            "rowId": "6",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "6",
                            "seatNo": "140",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "6",
                            "seatNo": "141",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "6",
                            "seatNo": "142",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "6",
                            "seatNo": "143",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "6",
                            "seatNo": "144",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "6",
                            "seatNo": "145",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "6",
                            "seatNo": "146",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "6",
                            "seatNo": "147",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "6",
                            "seatNo": "148",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "6",
                            "seatNo": "149",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "6",
                            "seatNo": "150",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "6",
                            "seatNo": "151",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "6",
                            "seatNo": "152",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "6",
                            "seatNo": "153",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "6",
                            "seatNo": "154",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "6",
                            "seatNo": "155",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "6",
                            "seatNo": "156",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "6",
                            "seatNo": "157",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "6",
                            "seatNo": "158",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "6",
                            "seatNo": "159",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "6",
                            "seatNo": "160",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "",
                            "rowId": "6",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "7",
                    "rowNum": 7,
                    "seats": [
                        {
                            "columnId": "",
                            "rowId": "7",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "7",
                            "seatNo": "163",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "7",
                            "seatNo": "164",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "7",
                            "seatNo": "165",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "7",
                            "seatNo": "166",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "7",
                            "seatNo": "167",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "7",
                            "seatNo": "168",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "7",
                            "seatNo": "169",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "7",
                            "seatNo": "170",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "7",
                            "seatNo": "171",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "7",
                            "seatNo": "172",
                            "seatStatus": 2,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "7",
                            "seatNo": "173",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "7",
                            "seatNo": "174",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "7",
                            "seatNo": "175",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "7",
                            "seatNo": "176",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "7",
                            "seatNo": "177",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "7",
                            "seatNo": "178",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "7",
                            "seatNo": "179",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "7",
                            "seatNo": "180",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "7",
                            "seatNo": "181",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "7",
                            "seatNo": "182",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "7",
                            "seatNo": "183",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "",
                            "rowId": "7",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "8",
                    "rowNum": 8,
                    "seats": [
                        {
                            "columnId": "",
                            "rowId": "8",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "8",
                            "seatNo": "186",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "8",
                            "seatNo": "187",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "8",
                            "seatNo": "188",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "8",
                            "seatNo": "189",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "8",
                            "seatNo": "190",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "8",
                            "seatNo": "191",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "8",
                            "seatNo": "192",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "8",
                            "seatNo": "193",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "8",
                            "seatNo": "194",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "8",
                            "seatNo": "195",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "8",
                            "seatNo": "196",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "8",
                            "seatNo": "197",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "8",
                            "seatNo": "198",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "8",
                            "seatNo": "199",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "8",
                            "seatNo": "200",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "8",
                            "seatNo": "201",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "8",
                            "seatNo": "202",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "8",
                            "seatNo": "203",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "8",
                            "seatNo": "204",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "8",
                            "seatNo": "205",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "8",
                            "seatNo": "206",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "",
                            "rowId": "8",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "9",
                    "rowNum": 9,
                    "seats": [
                        {
                            "columnId": "",
                            "rowId": "9",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "9",
                            "seatNo": "209",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "9",
                            "seatNo": "210",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "9",
                            "seatNo": "211",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "9",
                            "seatNo": "212",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "9",
                            "seatNo": "213",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "9",
                            "seatNo": "214",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "9",
                            "seatNo": "215",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "9",
                            "seatNo": "216",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "9",
                            "seatNo": "217",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "9",
                            "seatNo": "218",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "9",
                            "seatNo": "219",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "9",
                            "seatNo": "220",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "9",
                            "seatNo": "221",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "9",
                            "seatNo": "222",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "9",
                            "seatNo": "223",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "9",
                            "seatNo": "224",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "9",
                            "seatNo": "225",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "9",
                            "seatNo": "226",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "9",
                            "seatNo": "227",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "9",
                            "seatNo": "228",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "9",
                            "seatNo": "229",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "",
                            "rowId": "9",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "10",
                    "rowNum": 10,
                    "seats": [
                        {
                            "columnId": "",
                            "rowId": "10",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "10",
                            "seatNo": "232",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "10",
                            "seatNo": "233",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "10",
                            "seatNo": "234",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "10",
                            "seatNo": "235",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "10",
                            "seatNo": "236",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "10",
                            "seatNo": "237",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "10",
                            "seatNo": "238",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "10",
                            "seatNo": "239",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "10",
                            "seatNo": "240",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "10",
                            "seatNo": "241",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "10",
                            "seatNo": "242",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "10",
                            "seatNo": "243",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "10",
                            "seatNo": "244",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "10",
                            "seatNo": "245",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "10",
                            "seatNo": "246",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "10",
                            "seatNo": "247",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "10",
                            "seatNo": "248",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "10",
                            "seatNo": "249",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "10",
                            "seatNo": "250",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "10",
                            "seatNo": "251",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "10",
                            "seatNo": "252",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "",
                            "rowId": "10",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        }
                    ]
                },
                {
                    "rowId": "11",
                    "rowNum": 11,
                    "seats": [
                        {
                            "columnId": "22",
                            "rowId": "11",
                            "seatNo": "254",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "21",
                            "rowId": "11",
                            "seatNo": "255",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "20",
                            "rowId": "11",
                            "seatNo": "256",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "19",
                            "rowId": "11",
                            "seatNo": "257",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "18",
                            "rowId": "11",
                            "seatNo": "258",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "17",
                            "rowId": "11",
                            "seatNo": "259",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "16",
                            "rowId": "11",
                            "seatNo": "260",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "15",
                            "rowId": "11",
                            "seatNo": "261",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "14",
                            "rowId": "11",
                            "seatNo": "262",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "13",
                            "rowId": "11",
                            "seatNo": "263",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "12",
                            "rowId": "11",
                            "seatNo": "264",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "11",
                            "rowId": "11",
                            "seatNo": "265",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "10",
                            "rowId": "11",
                            "seatNo": "266",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "9",
                            "rowId": "11",
                            "seatNo": "267",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "8",
                            "rowId": "11",
                            "seatNo": "268",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "7",
                            "rowId": "11",
                            "seatNo": "269",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "6",
                            "rowId": "11",
                            "seatNo": "270",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "5",
                            "rowId": "11",
                            "seatNo": "271",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "4",
                            "rowId": "11",
                            "seatNo": "272",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "3",
                            "rowId": "11",
                            "seatNo": "273",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "2",
                            "rowId": "11",
                            "seatNo": "274",
                            "seatStatus": 1,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "1",
                            "rowId": "11",
                            "seatNo": "275",
                            "seatStatus": 4,
                            "seatType": "N",
                            "sectionId": "1"
                        },
                        {
                            "columnId": "",
                            "rowId": "11",
                            "seatNo": "",
                            "seatStatus": 0,
                            "seatType": "",
                            "sectionId": "1"
                        }
                    ]
                }
            ],
            // seats:null,
            selectedArr:[]
        };
    },
    computed: {
        showBtn(){
            let len = this.selectedArr.length;
            return len==0 ? true : false;
        },
        // bestRecommendation(){
        //     return Object.keys(this.seatData.seat.bestRecommendation)
        // }
    },
    watch:{
        selectedArr(){
            let len = this.selectedArr.length;
            if(len==0){
                this.btnText = '请先选座';
            }else{
                this.btnText = `￥${(this.price*10)*(len*10)/100} 确认选座`
                // this.btnText = `￥${(this.price*len).toFixed(1)} 确认选座`
            }
        }
    },
    methods:{
        // chooseBestRecommend(num){
        //     let best = this.seatData.seat.bestRecommendation;
        //     if(num==0){
        //         let bestOne = best.bestOne.seats;
        //         this.goBestRecommend(bestOne);
        //     }else if(num==1){
        //         let bestTwo = best.bestTwo.seats;
        //         this.goBestRecommend(bestTwo);
        //     }else if(num==2){
        //         let bestThree = best.bestThree.seats;
        //         this.goBestRecommend(bestThree);
        //     }else if(num==3){
        //         let bestFour = best.bestFour.seats;
        //         this.goBestRecommend(bestFour);
        //     }else if(num==4){
        //         let bestFive = best.bestFive.seats;
        //         this.goBestRecommend(bestFive);
        //     }
            
        // },
        // goBestRecommend(arr){
        //     arr.forEach((item)=>{

        //         this.seats.forEach((row,index)=>{
        //             if(item.rowId==row.rowId){

        //                 row.columns.forEach((col,i)=>{
        //                     if(item.columnId == col.columnId){
        //                         this.setSeat(index,i,SELECT)
        //                         this.selectedArr.push({
        //                             rowIndex:index,
        //                             colIndex:i,
        //                             seatNo:col.seatNo,
        //                             position:this.position(index,row.rowId,i,col.seatNo)
        //                         });
        //                     }
        //                 })
        //             }
        //         })
        //     })
        // },
        position(row,rowId,col,seatNo){
            let colseat = 0;
            let colArr = this.seats[row].seats.filter((item)=>item.seatNo!=='');
            // let colArr = this.seats[row].columns.filter((item)=>item.seatNo!=='');
            colArr.forEach((item,index)=>{
                if(item.seatNo==seatNo){
                    colseat = index+1;
                }
            })
            return `${rowId}排${colseat}座`
        },
        selectSeat(rowIndex,rowId,colIndex,seatType,seatNo){
            // let maxLen = this.bestRecommendation.length;
            console.log("rowIndex",rowIndex)
            console.log("rowId",rowId)
            console.log("colIndex",colIndex)
            console.log("seatType",seatType)
            console.log("seatNo",seatNo)
            let maxLen = 5;
            if(this.selectedArr.length>=maxLen && seatType == NOT_SELECT){
                this.$toast({
                    message: `每次最多可选${maxLen}个座位`,
                    duration: 3000
                });
                return;
            }
            
            if(seatType == NOT_SELECT && seatType !== EMPTY){
                this.setSeat(rowIndex,colIndex,SELECT); //?
                this.selectedArr.push({
                    rowIndex,
                    colIndex,
                    seatNo,
                    position:this.position(rowIndex,rowId,colIndex,seatNo)
                });
            }else if(seatType == SELECT){
                console.log("选票")
                this.setSeat(rowIndex,colIndex,NOT_SELECT)
                this.selectedArr.forEach((item,index,arr)=>{
                    if(item.seatNo===seatNo){
                        console.log("选票相同")
                        arr.splice(index,1);
                        return;
                    }
                })
            }else{
                return;
            }
        },
        setSeat(rowIndex,colIndex,state){
            let seatObj = this.seats[rowIndex].seats[colIndex];

            // let seatObj = this.seats[rowIndex].columns[colIndex];//
            // this.$set(seatObj,'st',state);
            this.$set(seatObj,'seatType',state);
        },
        deleteSelect(i){
            let selectedArr = this.selectedArr;
            let rowIndex = selectedArr[i].rowIndex;
            let colIndex = selectedArr[i].colIndex;
            this.setSeat(rowIndex,colIndex,NOT_SELECT);
            selectedArr.splice(i,1);
        },
        isLogin(){
            if(this.app.loginStatus==false){
                this.$messagebox.confirm('',{
                    message:'您需要登录才能购票哦！',
                    confirmButtonText:'去登录',
                    cancelButtonText:'留在这里'
                }).then(()=> {
                    this.$router.push('/login');
                }).catch(()=>{})
            }else{
                this.submitSelect();
            }
        },
        submitSelect(){
            let date = this.seatData.show.showDate.split('-');
            let sceneDate = `${date[1]}月${date[2]}日`;
            let orderInfo = {
                cinemaName:this.seatData.cinema.cinemaName,
                movieName:this.seatData.movie.movieName,
                sceneDate,
                sceneTime:this.seatData.show.showTime,
                lang:this.seatData.show.lang + this.seatData.show.dim,
                hallName:this.seatData.hall.hallName,
                payTime:new Date().toLocaleString(),
                selectedArr:this.selectedArr
            }
            this.$messagebox.confirm('o(>ω<)o确定购票吗?').then(()=> {
                this.$emit('update-payorder',orderInfo);
                this.$toast({
                    message: '购票成功，请在电影订单查看！',
                    duration: 1500
                });
                this.selectedArr.forEach((item)=>{
                    this.setSeat(item.rowIndex,item.colIndex,LK);
                })
                this.selectedArr = [];
                
            }).catch(()=> {
                this.$toast({
                    message: ' (╥╯^╰╥)呜呜呜',
                    duration: 1500
                });
            });
        }
    },
    created() {
        this.$indicator.open({
            text: '加载中...',
            spinnerType: 'triple-bounce'
        });
        let date = new Date().getTime();
        //http://m.maoyan.com/ajax/seatingPlan?timestamp=1551935723901
        this.$axios.post('/api/ajax/seatingPlan?timestamp='+date,{
            cityId: 20,
            ci: 20,
            seqNo: this.$route.params.id
        })
            .then(res=>{
                console.log("200来了")
                if(res.status===200){
                    console.log(res.data)
                    // this.$indicator.close();
                    return res.data
                }else{
                    return 'error'
                }
            })
            .then(data=>{
                console.log("data.seatData")
                console.log(data.seatData)
                this.seatData = data.seatData;
                console.log(data.seatData.seat)
                // this.seats = this.seatData.seat.sections[0].seats;
                this.seats = this.seatData.seat.regions[0].rows;
                this.$indicator.close();
            })
    },
    beforeRouteEnter (to, from, next) {
        next(vm=>{
            vm.app.showBack = true;
        })
    },
}

</script>

<style lang="less" scoped>

.seats-page{
    z-index: 10;
    position: relative;
    font-size: 0px;
}
.info-block{
    z-index: 5;
    position: relative;
    padding: .24rem;
    background: #fff;

    .movie-name{
        font-size:.32rem;
        font-weight:600;
        color:#333;
    }

    .show-info{
        margin-top: .1rem;

        >span{
            font-size: .26rem;
            color:#777;
            margin-right: .1rem;
        }
    }
}
.select-block{
    position: relative;
    height: 80vh;
    overflow-x: auto;
    text-align: center;

    .title{
        position: absolute;
        top: -12px;
        left: 40vh;
        text-align:center;
        padding: 12px 50px 0 50px;
        font-size: 14px;
        white-space: nowrap;
        color:#777;
        background: #e3e3e3;
        border-radius: 35px;
        transform: translateX(-50%);
    }

    .seats-block{
        position: relative;
        display: inline-block;
        padding: 0 1rem;
        margin-top: 1rem;
        opacity: .8;
    }

    .sideBar-num{
        position: fixed;
        display: inline-block;
        top:3.34rem;
        left:0;
        background: #e3e3e3;
        opacity: .8;

        .num{
            height: .3rem;
            padding: .1rem 0;
            font-size: .22rem;
            line-height: .3rem;
            color:#999;
            transform: scale(.8);
        }
    }

    .seats-row{
        display: flex;
        padding: 0.05rem 0;
    }

    .seats-col{
        width: .4rem;
        height: .4rem;
        margin-right: 0.06rem;

        &.N{
            background: url(../../public/img/seat-icon1.png) no-repeat;
            background-size: 100% 100%;
        }

        &.LK{
            background: url(../../public/img/seat-icon3.png) no-repeat;
            background-size: 100% 100%;
        }

        &.S{
            background: url(../../public/img/seat-icon2.png) no-repeat;
            background-size: 100% 100%;
        }
    }
}
.buy-block{
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;

    .seat-info{
        display:flex;
        justify-content: center;
        align-items: center;
        padding: 10px 0;
        background: #f5f5f5;

        .seat-type{
            font-size: 12px;
            color:#999;
            margin-right: 10px;

            &::before{
                content: '';
                display: inline-block;
                width: 17px;
                height: 15px;
                margin-right: 3px;
                vertical-align: top;
            }
        }

        .choose::before{            
            background: url(../../public/img/seat-icon1.png) no-repeat;
            background-size: 100% 100%;
        }

        .selected::before{
            background: url(../../public/img/seat-icon2.png) no-repeat;
            background-size: 100% 100%;
        }

        .sold::before{
            background: url(../../public/img/seat-icon3.png) no-repeat;
            background-size: 100% 100%;
        }

        .lover::before{
            background: url(../../public/img/seat-icon4.png) no-repeat;
            background-size: 100% 100%;
        }
    }

    .recommend-price-block{
        display:flex;
        align-items: center;
        padding: 10px;
        font-size: 12px;
        color:#999;
        background: #fff;

        .title{
            flex: 2;
            color:#333;
            font-size: 14px;
            margin-right: 5px;
        }

        .recommend{
            flex: 1;
            padding: 5px 8px;
            border:1px solid #ccc;
            margin-right: 5px;
            text-align: center;
        }

    }

    .selected-price-block{
        padding: 10px;
        padding-bottom: 0;
        background: #fff;

        .title{
            color:#333;
            font-size: 14px;
            margin-bottom: 5px;
        }

        .selected{
            display:flex;
             flex-wrap:wrap;

            .selected-item{
                position: relative;
                display:flex;
                flex-direction:column;
                margin: 0 3px 5px 0;
                padding: .05rem .35rem .05rem .12rem;
                font-size: .24rem;
                text-align: center;
                border-radius: 2px;
                border: 1px solid #ccc;
            }

            .position{
                color:#333;
            }

            .price{
                color:@red;
            }

            .delete{
                display: block;
                position:absolute;
                top:50%;
                right:0;
                padding: 3px;
                color:#ccc;
                transform: translateY(-50%);
            }
        }
    }

    .submit-block{
        padding: 10px;
        background: #fff;
    }
}
</style>