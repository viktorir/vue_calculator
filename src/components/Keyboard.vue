<template>
    <form class="keyboard">
        <button 
            type="button"
            class="button" 
            v-for="button in keyboard" 
            v-bind:key="button.id" 
            :id="button.id"
            @click="btnClick(button.id)"
        >{{ button.text }}</button>
    </form>

</template>

<script>
export default {
    props: {
        subWindowText: {
            type: String,
            required: true,
        },
        mainWindowText: {
            type: String,
            required: true,
        }
    },
    data() {
        return {
            keyboard: [
                {id: "null", text: "0"},
                {id: "one", text: "1"},
                {id: "two", text: "2"},
                {id: "three", text: "3"},                
                {id: "four", text: "4"},
                {id: "five", text: "5"},
                {id: "six", text: "6"}, 
                {id: "seven", text: "7"},
                {id: "eight", text: "8"},
                {id: "nine", text: "9"},

                {id: "cls", text: "C"},
                {id: "plus-minus", text: "±"},
                {id: "exp", text: "xʸ"},

                {id: "dot", text: "."},                
                {id: "div", text: "/"},
                {id: "multiply", text: "*"},
                {id: "minus", text: "-"},
                {id: "plus", text: "+"},
                {id: "eq", text: "="},
            ],
        }
    },
    methods: {
        btnClick(id) {
            this.$emit('btnClick', id);
            console.log('emit', id)
        }
    }
}
</script>

<style lang="scss" scoped>
.keyboard {
    width: 500px;
    height: 620px;

    margin-top: 20px;

    display: grid;
    grid-template-areas:
        "C PM EXP DIV"
        "SEV EIGHT NINE MLT"
        "FOUR FIVE SIX MIN"
        "ONE TWO THREE PLS"
        "NULL NULL DOT EQ";
    
        justify-items:center;
        align-items: center;
        gap: 20px;
}

.button {
    min-width: 100px;
    min-height: 100px;
    height: 100%;
    width: 100%;
    
    background-color: white;
    border: 1px solid #969072;
    border-radius: 20px;

    padding: 0;

    font-family: "Segoe UI";
    font-size: 48px;
}

#cls { 
    grid-area: C;
    color: #FFFFFF;
    background-color: #5766EB;
}
#eq { 
    grid-area: EQ; 
    background-color: #B6C2FD;
}

#plus-minus { grid-area: PM; }
#exp { grid-area: EXP; }
#div { grid-area: DIV; }
#seven { grid-area: SEV; }
#eight { grid-area: EIGHT; }
#nine { grid-area: NINE; }
#multiply { grid-area: MLT; }
#four { grid-area: FOUR; }
#five { grid-area: FIVE; }
#six { grid-area: SIX; }
#minus { grid-area: MIN; }
#one { grid-area: ONE; }
#two { grid-area: TWO; }
#three { grid-area: THREE; }
#plus { grid-area: PLS; }
#null { grid-area: NULL; }
#dot { grid-area: DOT; }

</style>