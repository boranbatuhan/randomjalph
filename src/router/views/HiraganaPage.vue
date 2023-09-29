<template>
    <div class="">
        <div class="contain  bg-[#0C0A08]">
            <!-- header -->
            <div class="item group">
                <p @click="goHome" class="group-hover:scale-105 transition-all cursor-pointer">hiragana</p>
            </div>
            <!-- section -->

            <div class="w-full h-full flex items-center justify-center flex-col flex-wrap gap-10 pb-16">
                <!-- hiragana table -->

                <HiraganaTable :checkSelected="checkSelected" :selectLetter="selectLetter" :selectAll="selectAll" :selectClear="selectClear" :isOpen="isOpen" ></HiraganaTable>
                <!-- set letters button  -->
                <button v-if="!isSet" @click="setLetters" :class="{'pointer-events-none':selected.length<=0}" class="border px-3 py-1.5  flex items-center justify-center neou bg-[#390097] hover:bg-[#7017ff] transition-all hover:-mt-2  ">
                        <p class="text-2xl text-white font-bold flex items-center justify-center gap-2">
                            set {{ selected.length }} letters
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 1024 1024"><path fill="currentColor" d="M77.248 415.04a64 64 0 0 1 90.496 0l226.304 226.304L846.528 188.8a64 64 0 1 1 90.56 90.496l-543.04 543.04l-316.8-316.8a64 64 0 0 1 0-90.496z"/></svg>
                        </p>
                </button>
                <!-- shuffleresult -->
                <div v-if="isSet" class="flex items-center justify-center gap-10">
                    <!-- shuffle card -->
                    <div  class="w-64 h-80  border md:mx-0 mx-auto flex items-center flex-col pt-12 bg-[#390097]">
                        <div id="resultContainer" @click="shuffleLetter" class="border w-40 h-24 cursor-pointer group relative  flex items-center justify-center neou bg-[#390097] ">
                            <p class="text-4xl text-white font-bold ">{{ result }}</p>
                            <p class="text-4xl text-white font-bold mt-7  invisible group-hover:visible transition-all neou absolute -bottom-12 bg-[#390097] px-4 py-2 ">{{ resultHiragana }}</p>
                        </div>
                        <button id="shuffleBtn" @click="shuffleLetter" class="bg-[#390097] border-[#00F171] hover:border-[#390097] hover:bg-[#00F171] border text-white font-semibold px-3 py-1.5 rounded-lg mt-auto mb-4 neou-btn flex items-center justify-center gap-2 " >
                            Shuffle
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M10.59 9.17L5.41 4L4 5.41l5.17 5.17l1.42-1.41zM14.5 4l2.04 2.04L4 18.59L5.41 20L17.96 7.46L20 9.5V4h-5.5zm.33 9.41l-1.41 1.41l3.13 3.13L14.5 20H20v-5.5l-2.04 2.04l-3.13-3.13z"/></svg>
                        </button>
                    </div>
                    <!-- drawning area -->
                    <DrawingArea ref="drawingAreaRef" :resultHiragana="resultHiragana" :shuffleLetter="shuffleLetter"/>
                </div>



        </div>
        </div>
    </div>
</template>

<script setup>
import router from '/src/router';
import { onMounted, ref } from 'vue';

import HiraganaTable from '/src/components/HiraganaTable.vue';
import DrawingArea from '/src/components/DrawingArea.vue';
const selected = ref([])
const selectedHiragana = ref([])
const result = ref("")
const resultHiragana = ref("")
const isSet = ref(false)
const isOpen = ref(true)

//drawing area ref
const drawingAreaRef=ref(null)

//go home func
const goHome=()=>{
    router.push("/")
}

//checker for cards
const setLetters=()=>{
    isOpen.value=false
    isSet.value=true
    document.addEventListener('keydown', function(event) {
            if (event.key == 's' && event.repeat === false ) {
                if(isSet.value){
                    shuffleLetter()
                }
            }
        });
}

//select letter unselect
const selectLetter=(name,hiragana)=>{

    if(checkSelected(name)){
        selected.value =  selected.value.filter(i => i != name)
        selectedHiragana.value =  selectedHiragana.value.filter(i => i != hiragana)
        isSet.value=false
    }
    else{
        selected.value.push(name)
        selectedHiragana.value.push(hiragana)
        isSet.value=false
    }
}

// letter click check
const checkSelected =(name)=>{
return selected.value.includes(name)
}


// same index checker
let lastIndex = -1;
const randomIndex = (uzunluk) => {
    let newIndex;
    do {
        newIndex = Math.floor(Math.random() * uzunluk);
    } while (newIndex === lastIndex);
    lastIndex = newIndex;
    return newIndex;
};

//random letter
const shuffleLetter = ()=>{

    //clear canvas - drawingArea component
    drawingAreaRef.value.clearCanvas()

    const container = document.querySelector("#resultContainer")
    const shuffleBtn = document.querySelector("#shuffleBtn")
    //result flip animation
    container.classList.add("flipping")
    shuffleBtn.classList.add("!pointer-events-none")
    setTimeout(() => {
        container.classList.remove("flipping")
        shuffleBtn.classList.remove("!pointer-events-none")
    }, 500);
    //random letter
    const length = selected.value.length 
    const index = randomIndex(length);
    // const index = Math.floor(Math.random() * length)

    result.value = selected.value[index]
    resultHiragana.value = selectedHiragana.value[index]

}

//Select all letter  ----- !!!!!!!!!!! Do not confuse the order of letters. !!!!!!!!!
const selectAll=()=>{
    selected.value=[ "a", "ka", "sa", "ta", "na", "ha", "ma", "ya", "ra", "wa", "i", "ki", "shi", "chi", "ni", "hi", "mi", "ri", "wi", "u", "ku", "su", "tsu", "nu", "fu", "mu", "yu", "ru", "e", "ke", "se", "te", "ne", "he", "me", "re", "we", "o", "ko", "so", "to", "no", "ho", "mo", "yo", "ro", "wo" ]
    selectedHiragana.value=[ "あ", "か", "さ", "た", "な", "は", "ま", "や", "ら", "わ", "い", "き", "し", "ち", "に", "ひ", "み", "り", "ゐ", "う", "く", "す", "つ", "ぬ", "ふ", "む", "ゆ", "る", "え", "け", "せ", "て", "ね", "へ", "め", "れ", "ゑ", "お", "こ", "そ", "と", "の", "ほ", "も", "よ", "ろ", "を" ]

}

//delete selected letter
const selectClear=()=>{
    selected.value=[]
    selectedHiragana.value=[]
}

</script>


<style  scoped>
.flipping {
	-webkit-animation: flipping 0.4s cubic-bezier(0.455, 0.030, 0.515, 0.955) both;
	        animation: flipping 0.4s cubic-bezier(0.455, 0.030, 0.515, 0.955) both;
}
 @-webkit-keyframes flipping {
  0% {
    -webkit-transform: rotateX(0);
            transform: rotateX(0);
  }
  100% {
    -webkit-transform: rotateX(-360deg);
            transform: rotateX(-360deg);
  }
}
@keyframes flipping {
  0% {
    -webkit-transform: rotateX(0);
            transform: rotateX(0);
  }
  100% {
    -webkit-transform: rotateX(-360deg);
            transform: rotateX(-360deg);
  }
}


.neou{
box-shadow:  -10px 10px 1px #00cf61,
             10px -10px 1px #0fff7f;
}

.neou-btn{
box-shadow:  -5px 5px 1px #00F171,
             5px -5px 1px #00F171;
}
.neou-btn:hover{
box-shadow:  -5px 5px 1px #390097,
             5px -5px 1px #390097;
}

.contain{
    @apply
    container mx-auto 
    min-h-[100dvh] md:min-h-screen 
    flex items-center justify-start flex-col gap-4
}

.item{
    @apply
    w-full h-24 
    text-center
    text-white
    select-none transition-all
    font-japan-wave
    flex items-center justify-center flex-col
    text-4xl group-hover:font-bold
    uppercase
    before:content-[''] before:w-4 before:h-4 before:rounded-full before:bg-[#be0029]
    hover:before:scale-110 before:transition-all
}


</style>