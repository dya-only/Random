<script>
    import { draggable } from 'svelte-drag'
    
    let isOpen = true
    let resOpen = 'hidden'
    let start = 1
    let end = 10
    let count = 5
    let repeat = false
    let arr = [0, ]

    const onClickResult = () => {

       
        if (!repeat && count < end) {
            arr = []

            let k = 0
            while(k < count) {
                const n = Math.floor(Math.random() * end) + start
            
                if (! arr.find((e) => (e === n))) {
                    arr.push(n)
                    k++
                }
            }

            console.log(arr)
            resOpen = 'res-open fixed z-50 bg-white w-[300px] h-[200px] border-[1px] shadow-xl rounded-2xl flex flex-col justify-start items-center'
        }

        
    }
</script>

<img class="w-screen h-screen fixed object-cover" src={'https://9to5mac.com/?attachment_id=811090'} alt="">

{ #if isOpen }
<div class="contain w-screen h-screen flex justify-center items-center z-40">

    { #if resOpen !== 'hidden' }
        <div use:draggable class={resOpen}>
            <div class="w-[300px] h-[40px] mb-6 flex justify-start items-end">
                <button class="cursor-pointer ml-[20px] font-bold text-red-400 mr-2" on:click={ () => resOpen = 'hidden' }>●</button>
                <div class="cursor-pointer font-bold text-yellow-400 mr-2">●</div>
                <div class="cursor-pointer font-bold text-green-400">●</div>
            </div>

            <div class="w-[280px] h-[125px] p-4 bg-slate-100 rounded-2xl flex flex-wrap justifty-start items-start">
                { #each arr as item, idx }
                    <div class="font-bold text-red-400 text-2xl m-2">{ item }</div>
                { /each }
            </div>
        </div>
    { /if }

    <div use:draggable class="bg-white w-[390px] h-[440px] border-[1px] shadow-xl rounded-2xl flex flex-col justify-start items-center">
        <div class="w-[400px] h-[40px] mb-6 flex justify-start items-end">
            <button class="cursor-pointer ml-7 font-bold text-red-400 mr-2" on:click={ () => isOpen = false }>●</button>
            <div class="cursor-pointer font-bold text-yellow-400 mr-2">●</div>
            <div class="cursor-pointer font-bold text-green-400">●</div>
        </div>

        <div class="w-[300px] flex flex-col justify-center items-start mb-16">
            <div class="mb-4 text-xl text-slate-500"><span class="text-blue-500 font-bold">어디까지</span> 필요한가요?</div>
            <div class="flex justify-center items-center">
                <input type="text" bind:value={start} class="w-24 h-12 p-4 rounded-2xl outline-none border-[0.5px] border-slate-200 transition duration-300 focus:border-blue-400" placeholder="시작" />
                <span class="ml-4 mr-4 font-bold text-slate-500">부터</span>
                <input type="text" bind:value={end} class="w-24 h-12 p-4 rounded-2xl outline-none border-[0.5px] border-slate-200 transition duration-300 focus:border-blue-400" placeholder="끝" />
            </div>
        </div>
    
        <div class="w-[300px] flex flex-col justify-center items-end mb-16">
            <div class="mb-4 text-xl text-slate-500"><span class="text-blue-500 font-bold">몇개를 </span>가져와야하나요?</div>
            <div class="flex justify-center items-center">
                <input type="text" bind:value={count} class="w-24 h-12 p-4 rounded-2xl outline-none border-[0.5px] border-slate-200 transition duration-300 focus:border-blue-400" placeholder="개수" />
                <span class="ml-4 font-bold text-slate-500">개</span>
            </div>
        </div>
    
        <button class="w-[300px] h-10 rounded-lg bg-blue-400 text-white font-bold outline-0 transition duration-200 active:scale-95" on:click={onClickResult}>결과 확인하기</button>
    </div>
</div>
{ /if }

<div class="w-56 h-24 backdrop-blur-2xl bg-white z-50 fixed"></div>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Lexend:wght@300;400;500;600;700;800;900&family=Noto+Sans+KR:wght@400;500;700;900&display=swap');
    
    .contain {
        font-family: 'Noto Sans KR', sans-serif;
    }
</style>