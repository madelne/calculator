<script>
export default {
    data() {
        return {
            result: '',
            log: []
        }
    },
    methods: {
        addToString(value) {
            this.result = this.result + value;
        },
        clearString() {
            this.result = '';
        },
        calculate() {
            try {
                const calculation = eval(this.result);
                
                if(this.result.includes('//')){
                    return this.updateResult('Enter a valid expression')
                }
                if (this.result.includes('/0')){
                    return this.updateResult('Division by zero is not allowed');
                }
                
                this.log.push(this.result + ' = ' + calculation);
                this.updateResult(calculation);
            } catch (error) {return this.updateResult('Enter a valid expression');}
        },
        updateResult(calculation) {
            this.result = calculation.toString();
        }
    }
}
</script>


<template>
    <div class="container">
        <div class="header">
            <h2>Calculator!</h2>
        </div>
        <div class="calculator">
            <button id="zero" @click="addToString(0)">0</button>
            <button id="one" @click="addToString(1)">1</button>
            <button id="two" @click="addToString(2)">2</button>
            <button id="three" @click="addToString(3)">3</button>
            <button id="four" @click="addToString(4)">4</button>
            <button id="five" @click="addToString(5)">5</button>
            <button id="six" @click="addToString(6)">6</button>
            <button id="seven" @click="addToString(7)">7</button>
            <button id="eight" @click="addToString(8)">8</button>
            <button id="nine" @click="addToString(9)">9</button>
            <button id="clear" @click="clearString">AC</button>
            <button id="comma" @click="addToString('.')">,</button>
            <button id="add" @click="addToString('+')">+</button>
            <button id="sub" @click="addToString('-')">-</button>
            <button id="mul" @click="addToString('*')">*</button>
            <button id="div" @click="addToString('/')">/</button>
            <button id="equ" @click="calculate">=</button>
            <div id="result">
                <p> {{ result }} </p>    
            </div>
                
        </div>
        <div class="history">
            <h5>History</h5>
            <ul>
                <li v-for="(history, index) in log" :key="index">
                    {{ history }}
                </li>
            </ul>
        </div>
    </div>
</template>
