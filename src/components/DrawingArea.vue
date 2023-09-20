<template>
    <div class="w-64 h-80  border bg-[#390097] border-[#00F171] flex items-center flex-col pb-8 gap-2">
      <div class=" text-white hover:text-[#00F171] cursor-pointer ml-auto m-2 relative group">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 36 36"><path fill="currentColor" d="M25.39 25.45a1 1 0 0 0-1.38.29c-1.41 2.16-4 4.81-6.31 5.7s-4.12.57-4.84 0c-.31-.27-1.12-1-.43-3.49c.46-1.66 3.32-9.48 4-11.38l-2.18.28c-.69 1.86-3.29 8.84-3.76 10.58c-.68 2.49-.34 4.3 1.09 5.56A5.59 5.59 0 0 0 15 34a9.53 9.53 0 0 0 3.45-.7c2.79-1.09 5.72-4.12 7.26-6.47a1 1 0 0 0-.32-1.38Z" class="clr-i-outline clr-i-outline-path-1"/><path fill="currentColor" d="M19.3 11a4.5 4.5 0 1 0-4.5-4.5a4.5 4.5 0 0 0 4.5 4.5Zm0-7a2.5 2.5 0 1 1-2.5 2.5A2.5 2.5 0 0 1 19.3 4Z" class="clr-i-outline clr-i-outline-path-2"/><path fill="currentColor" d="M11.81 15c.06 0 6.27-.82 7.73-1c.65-.1 1.14 0 1.3.15s.21.8-.07 1.68c-.61 1.86-3.69 11-4.59 13.71a8 8 0 0 0 1.29-.38a7.32 7.32 0 0 0 1.15-.6c1.23-3.56 3.53-10.46 4.05-12.04s.39-2.78-.3-3.6a3.16 3.16 0 0 0-3.08-.83c-1.43.15-7.47.94-7.73 1a1 1 0 0 0 .26 2Z" class="clr-i-outline clr-i-outline-path-3"/><path fill="none" d="M0 0h36v36H0z"/></svg>
        <div id="hint" class="w-48 h-44 bg-white/70 absolute top-11 right-5 invisible group-hover:visible transition-all !text-black text-9xl flex items-center justify-center pointer-events-none"> {{ props.resultHiragana }}</div>
      </div>
        <div class="w-52 h-48 bg-white border border-[#00F171]  neou">
            <canvas id="canvas" class="w-52 h-48"></canvas>
        </div>
       <div class="flex items-center justify-evenly w-full">
        <button @click="clearCanvas" class="bg-[#390097] border-[#00F171] hover:border-[#390097] hover:bg-[#00F171] border mt-4 text-white font-semibold px-3 py-1.5 rounded-lg  neou-btn  flex items-center justify-center gap-2" >
          Clear
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 48 48"><g fill="none" stroke="currentColor"><path stroke-linejoin="round" stroke-width="4.302" d="M44.782 24.17L31.918 7.1L14.135 20.5L27.5 37l3.356-2.336L44.782 24.17Z"/><path stroke-linejoin="round" stroke-width="4.302" d="m27.5 37l-3.839 3.075l-10.563-.001l-2.6-3.45l-6.433-8.536L14.5 20.225"/><path stroke-linecap="round" stroke-width="4.5" d="M13.206 40.072h31.36"/></g></svg>
        </button>
        <button @click="nextLetter" class="bg-[#390097] border-[#00F171] hover:border-[#390097] hover:bg-[#00F171] border mt-4 text-white font-semibold px-3 py-1.5 rounded-lg  neou-btn  flex items-center justify-center gap-2" >
          Next
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="none" stroke="currentColor" stroke-width="2" d="M2 12h20m-9-9l9 9l-9 9"/></svg>
        </button>
       </div>
    </div>
</template>

<script setup>
import { onMounted } from "vue";

//send func to parent
defineExpose({
    clearCanvas
})

// hiragana for hint
const props = defineProps({
  resultHiragana:String,
  shuffleLetter:Function
})

// clear canvas 
function clearCanvas() {
    const context = canvas.getContext("2d");
    context.clearRect(0, 0, canvas.width, canvas.height);
}
const nextLetter =()=>{
  const hint = document.querySelector('#hint')
  hint.classList.remove('invisible')
  setTimeout(() => {
    hint.classList.add('invisible')
    setTimeout(() => {
      clearCanvas()
    }, 100);
    setTimeout(() => {
      props.shuffleLetter()
    }, 200);
  }, 1500);
}

onMounted(()=>{  
    const canvas = document.getElementById("canvas");
    const context = canvas.getContext("2d");
    let isDrawing = false;
    let lastX = 0;
    let lastY = 0;
    const lineThickness = 4; 
    canvas.width = 13 * 16; //13rem * 16px
    canvas.height = 12 * 16; //12rem * 16px
    canvas.addEventListener("mousedown", startDrawing);
    canvas.addEventListener("mousemove", draw);
    canvas.addEventListener("mouseup", stopDrawing);
    canvas.addEventListener("mouseout", stopDrawing);
    //start drawing
    function startDrawing(e) {
      isDrawing = true;
      [lastX, lastY] = [e.clientX - canvas.offsetLeft, e.clientY - canvas.offsetTop];
      context.beginPath();
      context.moveTo(lastX, lastY);
    }
    // drawing
    function draw(e) {
      if (!isDrawing) return;
      const x = e.clientX - canvas.offsetLeft;
      const y = e.clientY - canvas.offsetTop;
      const distance = Math.sqrt((x - lastX) ** 2 + (y - lastY) ** 2);
      const step = 2; // Daha düzgün bir çizgi için adım uzunluğu
      if (distance > step) {
          context.lineWidth = lineThickness;
        context.lineTo(x, y);
        context.stroke();
        context.beginPath();
        context.moveTo(x, y);
        lastX = x;
        lastY = y;
      }
    }
    // stop drawing
    function stopDrawing() {
      isDrawing = false;
      context.beginPath();
    }

})
</script>

<style scoped>
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

</style>