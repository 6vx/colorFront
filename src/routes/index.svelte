<script>
    let colorApiUrl = "https://ykk1jsg6ch.execute-api.us-west-2.amazonaws.com/jsonReplyHopefully?"
    let synonymApiUrl = "https://api.datamuse.com/words?ml="
    let searchTerm="COLOR";
    let bingbong = []
    let bongbing = ""
    let synCage;
    function findBongbing (obj) {
        bingbong = []
        console.log(obj)
        for (const property in obj) {
            bingbong.push({
                color: `${property}`,
                value: parseInt(`${obj[property]}`)
            })
            // console.log(bingbong)
            bingbong.sort(function (a, b) {
                return b.value - a.value;
            });
            // console.log(bingbong)
            bongbing = bingbong[0].color 
        }
    }

    function findDominantColor (obj) {
        let colorArray = []
        console.log(obj)
        for (const property in obj) {
            colorArray.push({
                color: `${property}`,
                value: parseInt(`${obj[property]}`)
            })
            // console.log(bingbong)
            colorArray.sort(function (a, b) {
                return b.value - a.value;
            });
            // console.log(bingbong)
            return colorArray[0].color
        }
       
    }

    async function getColors() {
        searchTerm = searchTerm.toUpperCase()
        let searchUrl = colorApiUrl + searchTerm
		const res = await fetch(searchUrl);
		const text = await res.text();

		if (res.ok) {
            findBongbing(JSON.parse(text))
			return text;
		} else {
			throw new Error(text);
		}
	}
    async function getColors2(term) {
        term = term.toUpperCase()
        let searchUrl = colorApiUrl + term
		const res = await fetch(searchUrl);
		const text = await res.text();
		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}

    async function getSynonyms() {
        searchTerm = searchTerm.toUpperCase()
        let searchUrl = synonymApiUrl + searchTerm + "&max=5"
		const res = await fetch(searchUrl);
		const text = await res.text();

		if (res.ok) {
            synCage = (JSON.parse(text))
            synCage.forEach(wordObject => {
             // couldn't get it tongiht. sorry. i'll figure it out later. 
                
            });
			return text;
		} else {
			throw new Error(text);
		}
	}
	
	let promise = getColors();
    let promise2 = getSynonyms();

	function handleClick() {
		promise = getColors();
        promise2 = getSynonyms();
	}

</script>

<svelte:head>
     <title>colorAPI</title>
</svelte:head>




<h1 id="{bongbing}">
    colorAPI
</h1>

<input id="{bongbing}" bind:value="{searchTerm}" type="text"><button on:click="{handleClick}">check</button>

<p>
    find magical color in text quickly and easily
</p>

<!-- {#await promise then value}
    <p>{bongbing}</p>
{/await} -->

<!-- {#await promise2 then value}
    {#each synCage as word}
        <p class={word.dominantColor}
        >{word.word} {word.dominantColor}</p>
    {/each}
{/await} -->


<style>
    :root {
        text-align: center;
        background-color: rgb(17, 17, 17);
        font-family: monospace;
        color: rgb(168, 168, 168);
        
    }
    h1 {
        background-color: rgb(63, 63, 63);
        
    }
    p {
        background-color: rgb(26, 26, 26);
    }
    input {
        background-color: black;
        color: white;
        margin-right: 15px;
        text-align: center;
    }
    button {
        background-color: black;
        color: white;
    }
    #U {
        color: lightblue;
    }
    #R {
        color: lightcoral;
    }
    #G {
        color: lightgreen;
    }
    #W {
        color: lightgoldenrodyellow;
    }
    #B {
        color: violet;
    }
</style>