<template>
    <h1>Vue Calculator by viktorir</h1>
    <div id="calc">
        <window id="subWindow">{{ subWindowText }}</window>
        <window id="mainWindow">{{ mainWindowText }}</window>
        <keyboard 
            id="keyboard" 
            :subWindowText="subWindowText"
            :mainWindowText="mainWindowText"
            @btnClick="main"
        />
    </div>
</template>

<script>
import Window from "@/components/Window.vue"
import Keyboard from './components/Keyboard.vue'

export default {
    components: {
        Window,
        Keyboard
    },
    data() {
        return {
            subWindowText: "",
            mainWindowText: "0",
            numType: "int"
        }
    },
    methods: {
        calcResult() {
            let num2 = Number(this.mainWindowText);
            let num1 = Number(this.subWindowText.substring(0, this.subWindowText.length - 2));
            switch (this.subWindowText[this.subWindowText.length - 1]) {
                case "+": return num1 + num2;
                case "-": return num1 - num2;
                case "*": return num1 * num2;
                case "/": return num1 / num2;
                case "^": return Math.pow(num1, num2);
                default: return num2;
            }
        },
        numBtnChange(num) {
            if (this.mainWindowText == "0") this.mainWindowText = `${num}`;
            else this.mainWindowText += `${num}`;
        },
        operandBtnChange(operand) {
            if (!this.subWindowText) {
                this.subWindowText = this.mainWindowText + ` ${operand}`;   
            } 
            else {
                this.subWindowText = this.calcResult() + ` ${operand}`;
            }
            this.mainWindowText = "0";
            this.numType = "int";
            
        },
        main(event) {
            console.log('main change!', event)
            switch (event) {
                case "null":
                    if (this.mainWindowText != "0") this.mainWindowText += "0";
                    break;

                case "one": return this.numBtnChange(1);
                case "two": return this.numBtnChange(2);
                case "three": return this.numBtnChange(3);
                case "four": return this.numBtnChange(4);
                case "five": return this.numBtnChange(5);
                case "six": return this.numBtnChange(6);
                case "seven": return this.numBtnChange(7);
                case "eight": return this.numBtnChange(8);
                case "nine": return this.numBtnChange(9);

                case "cls": 
                    if (this.mainWindowText != "0") this.mainWindowText = "0";
                    else this.subWindowText = "";
                    this.numType = "int";
                    break;
                case "plus-minus":
                    if (this.mainWindowText[0] != "-") this.mainWindowText = "-" + this.mainWindowText;
                    else this.mainWindowText = this.mainWindowText.substring(1);
                    break;
                case "dot":
                    if (this.numType == "int") {
                        this.mainWindowText += ".";
                        this.numType = "float";
                    }
                    break;
                
                case "plus": return this.operandBtnChange("+");
                case "minus": return this.operandBtnChange("-");
                case "multiply": return this.operandBtnChange("*");
                case "div": return this.operandBtnChange("/");
                case "exp": return this.operandBtnChange("^");

                case "eq": 
                    this.mainWindowText = this.calcResult();
                    this.subWindowText = "";
                    this.numType = "int";

                default:
                    break;
            }
        }
    }
}
</script>

<style lang="scss">
$border-color: #969072;
$bg-color: #C5D7F9;
$main-window-color: rgba(96, 120, 185, 1);
$sub-window-color: rgba(96, 120, 185, 0.5);

#app {
    display: flex;

    justify-content: center;
    flex-direction: column;
    align-items: center;
}

#calc {
    background-color: $bg-color;
    
    width: 540px;
    height: 838px;
    padding: 20px;

    border: 1px solid $border-color;
    border-radius: 25px;

    display: flex;
    flex-direction: column;
    align-items: center;

}

#subWindow {
    height: 56px;

    font-family: 'Segoe UI';
    font-size: 42px;
    color: $sub-window-color;
}

#mainWindow {
    height: 72x;

    font-family: 'Segoe UI';
    font-size: 54px;
    color: $main-window-color;
}
</style>