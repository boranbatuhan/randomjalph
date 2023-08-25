<template>
    <div> 
        <details class="border select-none transition-all overflow-auto" :open="isOpen" >
                    <summary class=" py-2 font-bold tracking-widest text-2xl w-auto px-10 text-center bg-[#390097] text-[#00F171]">Select letters | Hiragana Alphabet</summary>
                    <table class="text-2xl">
                        <thead class="bg-zinc-300">
                            <tr >
                            <th class="w-16 h-16">w-</th>
                            <th class="w-16 h-16">r-</th>
                            <th class="w-16 h-16">y-</th>
                            <th class="w-16 h-16">m-</th>
                            <th class="w-16 h-16">h-</th>
                            <th class="w-16 h-16">n-</th>
                            <th class="w-16 h-16">t-</th>
                            <th class="w-16 h-16">s-</th>
                            <th class="w-16 h-16">k-</th>
                            <th @click="selectAllCell" class="group hover:text-[#390097] cursor-pointer">
                                <svg v-if="!allSelected" class="scale-100 group-hover:scale-105 transition-all block group-hover:hidden" xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 48 48"><path fill="none" stroke="currentColor" stroke-linejoin="round" stroke-width="4" d="M18 6H8a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2Zm0 22H8a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V30a2 2 0 0 0-2-2ZM40 6H30a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2Zm0 22H30a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V30a2 2 0 0 0-2-2Z"/></svg>
                                <svg v-if="!allSelected" class="scale-100 group-hover:scale-105 transition-all hidden group-hover:block" xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 48 48"><mask id="ipTAllApplication0"><path fill="#00F171" stroke="#fff" stroke-linejoin="round" stroke-width="4" d="M18 6H8a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2Zm0 22H8a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V30a2 2 0 0 0-2-2ZM40 6H30a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2Zm0 22H30a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V30a2 2 0 0 0-2-2Z"/></mask><path fill="currentColor" d="M0 0h48v48H0z" mask="url(#ipTAllApplication0)"/></svg>
                                <svg v-if="allSelected"  class="scale-100 group-hover:scale-105 transition-all text-[#390097]" xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 48 48"><mask id="ipSAllApplication0"><path fill="#fff" stroke="#fff" stroke-linejoin="round" stroke-width="4" d="M18 6H8a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2Zm0 22H8a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V30a2 2 0 0 0-2-2ZM40 6H30a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2Zm0 22H30a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V30a2 2 0 0 0-2-2Z"/></mask><path fill="currentColor" d="M0 0h48v48H0z" mask="url(#ipSAllApplication0)"/></svg>
                            </th>
                            <th @click="selectAllClear" class="group hover:text-[#390097] cursor-pointer"> 
                                <svg class="scale-100 group-hover:scale-105 transition-all" xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 24 24"><path fill="currentColor" d="M12 16c1.671 0 3-1.331 3-3s-1.329-3-3-3s-3 1.331-3 3s1.329 3 3 3z"/><path fill="currentColor" d="M20.817 11.186a8.94 8.94 0 0 0-1.355-3.219a9.053 9.053 0 0 0-2.43-2.43a8.95 8.95 0 0 0-3.219-1.355a9.028 9.028 0 0 0-1.838-.18V2L8 5l3.975 3V6.002c.484-.002.968.044 1.435.14a6.961 6.961 0 0 1 2.502 1.053a7.005 7.005 0 0 1 1.892 1.892A6.967 6.967 0 0 1 19 13a7.032 7.032 0 0 1-.55 2.725a7.11 7.11 0 0 1-.644 1.188a7.2 7.2 0 0 1-.858 1.039a7.028 7.028 0 0 1-3.536 1.907a7.13 7.13 0 0 1-2.822 0a6.961 6.961 0 0 1-2.503-1.054a7.002 7.002 0 0 1-1.89-1.89A6.996 6.996 0 0 1 5 13H3a9.02 9.02 0 0 0 1.539 5.034a9.096 9.096 0 0 0 2.428 2.428A8.95 8.95 0 0 0 12 22a9.09 9.09 0 0 0 1.814-.183a9.014 9.014 0 0 0 3.218-1.355a8.886 8.886 0 0 0 1.331-1.099a9.228 9.228 0 0 0 1.1-1.332A8.952 8.952 0 0 0 21 13a9.09 9.09 0 0 0-.183-1.814z"/></svg>
                            </th>
                        </tr>
                    </thead>
                    <tbody  class="bg-blue-300">
                        <!-- AAAAAAA  -->
                        <tr>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('wa')}"  @click="selectLetter('wa')"><p class="text-4xl group-hover:font-bold">わ</p> <p class="text-sm select-none">wa</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ra')}"  @click="selectLetter('ra')"><p class="text-4xl group-hover:font-bold">ら</p> <p class="text-sm select-none">ra</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ya')}"  @click="selectLetter('ya')"><p class="text-4xl group-hover:font-bold">や</p> <p class="text-sm select-none">ya</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ma')}"  @click="selectLetter('ma')"><p class="text-4xl group-hover:font-bold">ま</p> <p class="text-sm select-none">ma</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ha')}"  @click="selectLetter('ha')"><p class="text-4xl group-hover:font-bold">は</p> <p class="text-sm select-none">ha</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('na')}"  @click="selectLetter('na')"><p class="text-4xl group-hover:font-bold">な</p> <p class="text-sm select-none">na</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ta')}"  @click="selectLetter('ta')"><p class="text-4xl group-hover:font-bold">た</p> <p class="text-sm select-none">ta</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('sa')}"  @click="selectLetter('sa')"><p class="text-4xl group-hover:font-bold">さ</p> <p class="text-sm select-none">sa</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ka')}"  @click="selectLetter('ka')"><p class="text-4xl group-hover:font-bold">か</p> <p class="text-sm select-none">ka</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('a')}"  @click="selectLetter('a')"><p class="text-4xl group-hover:font-bold">あ</p> <p class="text-sm select-none">a</p></div> </td>
                            <td class="font-bold">-a</td>
                        </tr>
                        <!-- iii  -->
                        <tr>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('wi')}"  @click="selectLetter('wi')"><p class="text-4xl group-hover:font-bold">ゐ</p> <p class="text-sm select-none">wi</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ri')}"  @click="selectLetter('ri')"><p class="text-4xl group-hover:font-bold">り</p> <p class="text-sm select-none">ri</p></div> </td>
                            <td> <div class="td group pointer-events-none"><p class="text-4xl group-hover:font-bold"></p> <p class="text-sm select-none"></p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('mi')}"  @click="selectLetter('mi')"><p class="text-4xl group-hover:font-bold">み</p> <p class="text-sm select-none">mi</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('hi')}"  @click="selectLetter('hi')"><p class="text-4xl group-hover:font-bold">ひ</p> <p class="text-sm select-none">hi</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ni')}"  @click="selectLetter('ni')"><p class="text-4xl group-hover:font-bold">に</p> <p class="text-sm select-none">ni</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('chi')}"  @click="selectLetter('chi')"><p class="text-4xl group-hover:font-bold">ち</p> <p class="text-sm select-none">chi</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('shi')}"  @click="selectLetter('shi')"><p class="text-4xl group-hover:font-bold">し</p> <p class="text-sm select-none">shi</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ki')}"  @click="selectLetter('ki')"><p class="text-4xl group-hover:font-bold">き</p> <p class="text-sm select-none">ki</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('i')}"  @click="selectLetter('i')"><p class="text-4xl group-hover:font-bold">い</p> <p class="text-sm select-none">i</p></div> </td>
                            <td class="font-bold">-i</td>
                        </tr>
                        <!-- uuu  -->
                        <tr>
                            <td> <div class="td group pointer-events-none"><p class="text-4xl group-hover:font-bold"></p> <p class="text-sm select-none"></p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ru')}"  @click="selectLetter('ru')"><p class="text-4xl group-hover:font-bold">る</p> <p class="text-sm select-none">ru</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('yu')}"  @click="selectLetter('yu')"><p class="text-4xl group-hover:font-bold">ゆ</p> <p class="text-sm select-none">yu</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('mu')}"  @click="selectLetter('mu')"><p class="text-4xl group-hover:font-bold">む</p> <p class="text-sm select-none">mu</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('fu')}"  @click="selectLetter('fu')"><p class="text-4xl group-hover:font-bold">ふ</p> <p class="text-sm select-none">fu</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('nu')}"  @click="selectLetter('nu')"><p class="text-4xl group-hover:font-bold">ぬ</p> <p class="text-sm select-none">nu</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('tsu')}"  @click="selectLetter('tsu')"><p class="text-4xl group-hover:font-bold">つ</p> <p class="text-sm select-none">tsu</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('su')}"  @click="selectLetter('su')"><p class="text-4xl group-hover:font-bold">す</p> <p class="text-sm select-none">su</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ku')}"  @click="selectLetter('ku')"><p class="text-4xl group-hover:font-bold">く</p> <p class="text-sm select-none">ku</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('u')}"  @click="selectLetter('u')"><p class="text-4xl group-hover:font-bold">う</p> <p class="text-sm select-none">u</p></div> </td>
                            <td class="font-bold">-u</td>
                        </tr>
                        <!-- eee  -->
                        <tr>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('we')}"  @click="selectLetter('we')"><p class="text-4xl group-hover:font-bold">ゑ</p> <p class="text-sm select-none">we</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('re')}"  @click="selectLetter('re')"><p class="text-4xl group-hover:font-bold">れ</p> <p class="text-sm select-none">re</p></div> </td>
                            <td> <div class="td group pointer-events-none"><p class="text-4xl group-hover:font-bold"></p> <p class="text-sm select-none"></p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('me')}"  @click="selectLetter('me')"><p class="text-4xl group-hover:font-bold">め</p> <p class="text-sm select-none">me</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('he')}"  @click="selectLetter('he')"><p class="text-4xl group-hover:font-bold">へ</p> <p class="text-sm select-none">he</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ne')}"  @click="selectLetter('ne')"><p class="text-4xl group-hover:font-bold">ね</p> <p class="text-sm select-none">ne</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('te')}"  @click="selectLetter('te')"><p class="text-4xl group-hover:font-bold">て</p> <p class="text-sm select-none">te</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('se')}"  @click="selectLetter('se')"><p class="text-4xl group-hover:font-bold">せ</p> <p class="text-sm select-none">se</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ke')}"  @click="selectLetter('ke')"><p class="text-4xl group-hover:font-bold">け</p> <p class="text-sm select-none">ke</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('e')}"  @click="selectLetter('e')"><p class="text-4xl group-hover:font-bold">え</p> <p class="text-sm select-none">e</p></div> </td>
                            <td class="font-bold">-e</td>
                        </tr>
                        <!-- ooo  -->
                        <tr>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('wo')}"  @click="selectLetter('wo')"><p class="text-4xl group-hover:font-bold">を</p> <p class="text-sm select-none">wo</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ro')}"  @click="selectLetter('ro')"><p class="text-4xl group-hover:font-bold">ろ</p> <p class="text-sm select-none">ro</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('yo')}"  @click="selectLetter('yo')"><p class="text-4xl group-hover:font-bold">よ</p> <p class="text-sm select-none">yo</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('mo')}"  @click="selectLetter('mo')"><p class="text-4xl group-hover:font-bold">も</p> <p class="text-sm select-none">mo</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ho')}"  @click="selectLetter('ho')"><p class="text-4xl group-hover:font-bold">ほ</p> <p class="text-sm select-none">ho</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('no')}"  @click="selectLetter('no')"><p class="text-4xl group-hover:font-bold">の</p> <p class="text-sm select-none">no</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('to')}"  @click="selectLetter('to')"><p class="text-4xl group-hover:font-bold">と</p> <p class="text-sm select-none">to</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('so')}"  @click="selectLetter('so')"><p class="text-4xl group-hover:font-bold">そ</p> <p class="text-sm select-none">so</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('ko')}"  @click="selectLetter('ko')"><p class="text-4xl group-hover:font-bold">こ</p> <p class="text-sm select-none">ko</p></div> </td>
                            <td> <div class="td group" :class="{'!font-bold !bg-[#390097] !text-[#00F171]':checkSelected('o')}"  @click="selectLetter('o')"><p class="text-4xl group-hover:font-bold">お</p> <p class="text-sm select-none">o</p></div> </td>
                            <td class="font-bold">-o</td>
                        </tr>

                    </tbody>
                </table>
            </details>
    </div>
</template>

<script setup>
import { ref } from "vue"


const props=defineProps({
    checkSelected:Function,
    selectLetter:Function,
    selectAll:Function,
    selectClear:Function,
    isOpen:Boolean
})

const allSelected = ref(false)

const selectAllCell = ()=>{
 allSelected.value= true

    props.selectAll()
}
const selectAllClear = ()=>{
 allSelected.value= false
 props.selectClear()
}
</script>

<style scoped>

th{
    @apply
    px-3 py-1
    even:bg-pink-300/20  odd:bg-pink-700/20  
}

.td{
    @apply
    flex items-center justify-center flex-col
    w-16 h-16
    px-3 py-1
    even:bg-pink-300/20  odd:bg-pink-700/20  
    cursor-default
    hover:!bg-[#390097]/50 hover:!text-[#00F171]
    
}


summary {
  display: block;
}

summary::after {
    float: right;        
  margin-left: 2rem;
  content: '▶️';
  transition: 0.2s;
}
    
details[open] summary::after {
  transform: rotate(90deg);
}
</style>