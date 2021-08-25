<template lang="">
    <div class="container">
        <h1>계산기</h1>
        <div class="output">
            {{ display }}
        </div>
        <div class="buttons" @click="numfn('1')">1</div>
        <div class="buttons" @click="numfn('2')">2</div>
        <div class="buttons" @click="numfn('3')">3</div>
        <div class="buttons" @click="operator='+'">+</div>
        <div class="buttons" @click="numfn('4')">4</div>
        <div class="buttons" @click="numfn('5')">5</div>
        <div class="buttons" @click="numfn('6')">6</div>
        <div class="buttons" @click="operator='-'">-</div>
        <div class="buttons" @click="numfn('7')">7</div>
        <div class="buttons" @click="numfn('8')">8</div>
        <div class="buttons" @click="numfn('9')">9</div>
        <div class="buttons" @click="operator='*'">*</div>
        <div class="buttons" @click="clear('C')">C</div>
        <div class="buttons" @click="numfn('0')">0</div>
        <div class="buttons" @click="cal('=')">=</div>
        <div class="buttons" @click="operator='/'">/</div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            // +,-,*,/ 연산자 기호 입력받기 전의 숫자를 저장하는 임시변수
            a: '',
            // +,-,*,/ 연산자 기호 입력받고 난 다음의 숫자를 저장하는 임시변수
            b: '',
            // 연산 결과값을 저장하는 변수(정수형)
            tot: 0,
            // 입력받은 내용이나 연산 결과를 브라우저 화면에 보여주기 위한 변수
            display: 0,
            // 입력받은 데이터가 연산자인가 아닌가 구별하기 위한 변수
            operator: null
        }
    },
    methods: {
        numfn(num){
            //  만약 입력받은 값이 연산자가 아니면
            if(this.operator === null){
                // 입력받은 데이터를 a변수에 저장(누적)
                this.a += num;
                // 입력받은 데이터를 브라우저 화면에 표시
                this.display = this.a;
            }
            // 입력받은 값이 연산자라면
            else{
                this.b += num;
                this.display = this.b;
            }
        },
        cal(){
            // switch~case문 작성
            // this.operator변수의 값이 + 이면 덧셈 연산...
            switch(this.operator){
                // parseFloat() : () 안의 데이터를 실수로 형변환
                // parseInt() : () 안의 데이터를 정수로 형변환
                case '+' : this.tot = parseFloat(this.a) + parseFloat(this.b);
                // switch~case문 빠져나감
                break;
                case '-' : this.tot = parseFloat(this.a) - parseFloat(this.b);
                break;
                case '*' : this.tot = parseFloat(this.a) * parseFloat(this.b);
                break;
                case '/' : this.tot = parseFloat(this.a) / parseFloat(this.b);
            }
            this.display = this.tot;
            this.a = '' + this.tot + '';
            this.b = '';
            this.operator = null;
        },
        //  clear함수가 호출되면 모든 변수 초기화
        clear(){
            this.a = '';
            this.b = '';
            this.tot = 0;
            this.display = 0;
            this.operator = null;
        }
    }
}
</script>
<style type="text/css">
    .container {
        width:360px;
        /*행과 열로 자식객체 나열*/
        display:grid;  
        /*grid 요소의 열의 배치를 자동으로 결정함*/
        grid-template-columns:auto auto auto auto;
        /*grid 요소의 간격 조절*/
        grid-gap:10px;
        background-color: #efefef;
        border-radius:10px;
        margin:50px auto;
        padding:20px;
    }
    .container h1 {
        text-align:center;
        width:100%;
        font-size:30px;
        grid-column:1/5;
        background-color:rgba(0,0,0,0.2);
        padding:10px 0;
        border-radius:10px;
    }
    .output {
        width:100%;
        /*output의 가로길이는 100%로 하고, buttons은 아래로 내려감*/
        grid-column:1/5;   /* 1/span 4 */
        background-color:#f6b93b;
        text-align:right;
        padding:10px 20px;
        font-size:30px;
        border-radius:10px;
        margin-bottom:10px;
        box-shadow:3px 3px 3px rgba(0,0,0,0.3);
        box-sizing:border-box;
    }
    .buttons {
        background-color:#4a69bd;
        text-shadow:1px 1px 1px #fff;
        font-size:24px;
        padding:14px 10px;
        border-radius:10px;
        text-align: center;
        cursor:pointer;
        box-shadow:3px 3px 3px rgba(0,0,0,0.3);
        color: #e55039;
    }
</style>