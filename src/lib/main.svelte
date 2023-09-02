<script lang="ts">
    interface Exercise {
    type: string;
    ex_name_1: string;
    ex_set_1: number;
    ex_count_1: number;
    ex_explain_1:string;
    ex_name_2: string;
    ex_set_2: number;
    ex_count_2: number;
    ex_explain_2:string;
    }

    let page = true
    let focus_name:string;
    let focus_explain:string;

    const change_page = (name:string,explain:string) => {
        focus_explain = explain
        focus_name = name
        page = false
    }

    const change_page2 = () => {
        page = true
    }

    let Data:Exercise[] = [];
        function getUrlParameter(name:string) {
        const urlParams = new URLSearchParams(window.location.search);
        return urlParams.get(name);
    }

    const paramValue = getUrlParameter('first');

    if (paramValue) {
        try {
            const parsedData = JSON.parse(paramValue);
            Data = parsedData
            console.log(Data)
            console.log('Received data:', parsedData,parsedData[0].ex_name);
        } catch (error) {
            console.error('Error parsing data:', error);
        }
    } else {
        console.error('No "first" parameter found in the URL.');
    }

</script>
<main>
    <div class="body">
        {#if page}
        {#each Data as value}
            <div class="container">
                <div class="type">
                    {value.type}
                </div>
                <button on:click={()=>change_page(value.ex_name_1,value.ex_explain_1)}>
                <div class="ex_box">
                    <div class="ex_name">
                        {value.ex_name_1}
                    </div>
                    <div class="ex_set">
                        {value.ex_set_1} 세트
                    </div>
                    <div class="ex_count">
                        세트당 {value.ex_count_1} 회
                    </div>
                </div>
            </button>
            <button on:click={()=>change_page(value.ex_name_2,value.ex_explain_2)}>
                <div class="ex_box">
                    <div class="ex_name">
                        {value.ex_name_2}
                    </div>
                    <div class="ex_set">
                        {value.ex_set_2}세트
                    </div>
                    <div class="ex_count">
                        세트당 {value.ex_count_2}회
                    </div>
                </div>
            </button>
            </div>
        {/each}
        {:else}
        <div class="flex">
            <div class="header">
            <button class="go_back" on:click={()=>change_page2()}>&nbsp;&nbsp;&lt; {focus_name}</button>
            </div>
            <div class="explain">{focus_explain}</div>
        </div>
        {/if}
    </div>
</main>
<style>
    * {
        user-select: none;
        overflow-y: auto;
    }

    .go_back {
        display: inline-block;
    }

    .flex{
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .header {
        width: 24.375rem;
        height: 4.5rem;
        flex-shrink: 0;
        background: var(--white, #FFF);
        color: var(--orange-600, #EA580C);
        text-align: center;
        font-family: SUITE;
        font-size: 1.25rem;
        font-style: normal;
        font-weight: 800;
        line-height: normal;
        letter-spacing: -0.025rem;
        height: 5vh;
        width: 100vw;
        top: 0;
    }

    .explain{
        display: inline-flex;
        padding: 1.25rem 1.5625rem;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 0.625rem;
        border-radius: 1.5625rem;
        background: #FFF;
        color: var(--orange-950, #431407);
        font-family: SUITE;
        font-size: 1.125rem;
        font-style: normal;
        width: 80vw;
        height: 80vh;
        margin-top: 10px;
        font-weight: 600;
        line-height: normal;
        letter-spacing: -0.0225rem;
    }

    main {
        display: flex;
        width: 100vw;
        height: 100vh;
        background: var(--orange-400, #fb923c);
        overflow-y: hidden;
        display: flex;
        justify-content: center;
    }

    .container{
        margin-top: 2vw;
        margin-bottom: 2vw;
        width: 80vw;
        padding: 20px;
        /* flex-shrink: 0; */
        border-radius: 1.5rem;
        background: var(--white, #FFF);
    }

    button {
    /* 모든 기본 스타일을 제거 */
    margin: 0;
    padding: 0;
    border: none;
    background: none;
    font: inherit;
    color: inherit;
    cursor: pointer;
    width: 100%;
    text-align: left;
}

    .type{
        color: var(--orange-700, #C2410C);
        font-family: SUITE;
        font-size: 1.25rem;
        font-style: normal;
        font-weight: 800;
        line-height: normal;
        letter-spacing: -0.025rem;
    }

    .ex_box{
        flex-shrink: 0;
        padding: 10px;
        border-radius: 1rem;
        border: 1px solid var(--orange-500, #F97316);
        background: var(--orange-50, #FFF7ED);
        margin-top: 20px;
    }

    .ex_name{
        color: var(--orange-600, #EA580C);
        font-family: SUITE;
        font-size: 1.125rem;
        font-style: normal;
        font-weight: 800;
        line-height: normal;
        letter-spacing: -0.0225rem;
        margin-bottom: 5px;
    }

    .ex_set{
        display: flex;
        padding: 0.5rem 0.75rem;
        justify-content: center;
        align-items: center;
        gap: 0.25rem;
        border-radius: 1rem;
        background: var(--orange-600, #EA580C);
        color: var(--white, #FFF);
        font-family: SUITE;
        font-size: 0.75rem;
        font-style: normal;
        font-weight: 800;
        line-height: normal;
        letter-spacing: -0.0075rem;
        display: inline-block;
        padding: 5px;
        padding-left: 8px;
        padding-right: 8px;
    }

    .ex_count{
        color: var(--orange-600, #EA580C);
        font-family: SUITE;
        font-size: 0.75rem;
        font-style: normal;
        font-weight: 800;
        line-height: normal;
        letter-spacing: -0.0075rem;
        display: flex;
        padding: 0.5rem 0.75rem;
        justify-content: center;
        align-items: center;
        gap: 0.25rem;
        border-radius: 1rem;
        border: 1px solid var(--orange-600, #EA580C);
        background: var(--orange-50, #FFF7ED);
        padding: 5px;
        display: inline-block;
        padding-left: 8px;
        padding-right: 8px;
    }
</style>    