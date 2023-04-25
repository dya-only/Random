<script>
    import { draggable } from 'svelte-drag'
    
    let isOpen = true
    let resOpen = 'hidden'
    let start = 1
    let end = 10
    let count = 5
    let repeat = true
    let arr = [0, ]

    const onClickResult = () => {
       
        if (repeat) {
            if (count < end) {
                arr = []
    
                let k = 0
                while(k < count) {
                    let n = Math.floor(Math.random() * end) + start
                
                    if (! arr.find((e) => (e === n))) {
                        arr.push(n)
                        k++
                    }
                }
    
                console.log(arr)
                resOpen = 'res-open fixed z-50 bg-white w-[300px] h-[200px] border-[1px] shadow-xl rounded-2xl flex flex-col justify-start items-center'
            }
        } else {
            arr = []
            
            for (let i = 0; i < count; i++) {
                arr.push(Math.floor(Math.random() * end) + start)
            }
            
            resOpen = 'res-open fixed z-50 bg-white w-[300px] h-[200px] border-[1px] shadow-xl rounded-2xl flex flex-col justify-start items-center'
        }
        
    }
</script>

<div class="loading fixed w-screen h-screen z-50 bg-blue-400 flex justify-center items-center">
  로딩중이에요...
</div>

<img class="w-screen h-screen fixed object-cover" src={'https://9to5mac.com/?attachment_id=811090'} alt="">
<div class="fixed m-8">
    <div class="text-xl text-white opacity-75 font-bold z-20">드래그 & 드롭해서 창을 움직여보세요</div>
    <div class="text-xl text-white opacity-75 font-bold z-20">닫기 버튼(<span class="text-red-400">빨간색</span>)을 클릭하여 닫을 수도 있어요</div>
</div>
<!-- <div class="m-8 text-xl text-white opacity-75 font-bold z-20">드래그 & 드롭해서 윈도우를 움직여보세요</div> -->

{ #if isOpen }
<div class="contain w-screen h-screen flex justify-center items-center z-40">
    
    { #if resOpen !== 'hidden' }
        <div use:draggable class={resOpen}>
            <div class="w-[300px] h-[40px] mb-6 flex justify-start items-end">
                <button class="cursor-pointer ml-[20px] font-bold text-red-400 mr-2" on:click={ () => resOpen = 'hidden' }>●</button>
                <div class="cursor-pointer font-bold text-yellow-400 mr-2">●</div>
                <div class="cursor-pointer font-bold text-green-400">●</div>
            </div>
            
            <div class="w-[280px] h-[125px] overflow-y-auto p-4 bg-slate-100 rounded-2xl flex flex-wrap justifty-start items-start">
                { #each arr as item, idx }
                    <div class="font-bold text-red-400 text-2xl m-2">{ item }</div>
                { /each }
            </div>
        </div>
    { /if }

    <div use:draggable class="bg-white w-[390px] h-[450px] border-[1px] shadow-xl rounded-2xl flex flex-col justify-start items-center">
        <div class="w-[400px] h-[40px] mb-6 flex justify-start items-end">
            <button class="cursor-pointer ml-7 font-bold text-red-400 mr-2" on:click={ () => isOpen = false }>●</button>
            <div class="cursor-pointer font-bold text-yellow-400 mr-2">●</div>
            <div class="cursor-pointer font-bold text-green-400">●</div>
        </div>

        <div class="w-[300px] flex flex-col justify-center items-start mb-16">
            <div class="mb-4 text-xl text-slate-500"><span class="text-blue-500 font-bold">어디까지</span> 필요한가요?</div>
            <div class="flex justify-center items-center">
                <!-- <input type="text" bind:value={start} class="w-24 h-12 p-4 rounded-2xl outline-none border-[0.5px] border-slate-200 transition duration-300 focus:border-blue-400" placeholder="시작" /> -->
                <input type="number" bind:value={end} class="w-24 h-12 p-4 rounded-2xl outline-none border-[0.5px] border-slate-200 transition duration-300 focus:border-blue-400" placeholder="끝" />
                <span class="ml-4 mr-4 font-bold text-slate-500">까지</span>
            </div>
        </div>
    
        <div class="w-[300px] flex flex-col justify-center items-end mb-12">
            <div class="mb-4 text-xl text-slate-500"><span class="text-blue-500 font-bold">몇개를 </span>가져와야하나요?</div>
            <div class="flex justify-center items-center">
                <input type="number" bind:value={count} class="w-24 h-12 p-4 rounded-2xl outline-none border-[0.5px] border-slate-200 transition duration-300 focus:border-blue-400" placeholder="개수" />
                <span class="ml-4 font-bold text-slate-500">개</span>
            </div>
        </div>

        <div class="w-[300px] flex justify-start items-center mb-2">
            <input type="checkbox" bind:checked={repeat} class="w-4 h-4 rounded-xl" placeholder="개수" />
            <span class="ml-4 font-bold text-slate-500">중복을 없애주세요!</span>
        </div>
    
        <button class="w-[300px] h-10 rounded-lg bg-blue-400 text-white font-bold outline-0 transition duration-200 active:scale-95" on:click={onClickResult}>결과 확인하기</button>
    </div>
</div>
{ /if }

<style>
    @import url('https://fonts.googleapis.com/css2?family=Lexend:wght@300;400;500;600;700;800;900&family=Noto+Sans+KR:wght@400;500;700;900&display=swap');
    
    .contain {
        font-family: 'Noto Sans KR', sans-serif;
    }
</style>