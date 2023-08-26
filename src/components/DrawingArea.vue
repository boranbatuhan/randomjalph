<template>
    <div class="w-64 h-80 border bg-[#390097] border-[#00F171] flex items-center flex-col py-8 gap-2">
        <div class="w-52 h-52 bg-white border border-[#00F171]  neou">
            <canvas id="canvas" class="w-52 h-52"></canvas>
        </div>
        <button @click="clearCanvas" class="bg-[#390097] border-[#00F171] hover:border-[#390097] hover:bg-[#00F171] border mt-4 text-white font-semibold px-3 py-1.5 rounded-lg  neou-btn " >Clear</button>

    </div>
</template>

<script setup>
import { onMounted } from "vue";

defineExpose({
    clearCanvas
})
function clearCanvas() {
    const context = canvas.getContext("2d");
    context.clearRect(0, 0, canvas.width, canvas.height);
}

onMounted(()=>{  
    const canvas = document.getElementById("canvas");
    const context = canvas.getContext("2d");
    let isDrawing = false;
    let lastX = 0;
    let lastY = 0;
    const lineThickness = 4; 
    canvas.width = 13 * 16; // 13rem * 16px/rem = genişlik piksel cinsinden
    canvas.height = 13 * 16; // 13rem * 16px/rem = yükseklik piksel cinsinden
    canvas.addEventListener("mousedown", startDrawing);
    canvas.addEventListener("mousemove", draw);
    canvas.addEventListener("mouseup", stopDrawing);
    canvas.addEventListener("mouseout", stopDrawing);
    function startDrawing(e) {
      isDrawing = true;
      [lastX, lastY] = [e.clientX - canvas.offsetLeft, e.clientY - canvas.offsetTop];
      context.beginPath();
      context.moveTo(lastX, lastY);
    }
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