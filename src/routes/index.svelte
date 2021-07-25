<script>
    let colorApiUrl = "https://ykk1jsg6ch.execute-api.us-west-2.amazonaws.com/jsonReplyHopefully?"
    let searchTerm="COLOR";
    let bingbong = []
    let bongbing = ""
    function findBongbing (obj) {
        bingbong = []
        console.log(obj)
        for (const property in obj) {
            bingbong.push({
                color: `${property}`,
                value: parseInt(`${obj[property]}`)
            })
            console.log(bingbong)
            bingbong.sort(function (a, b) {
                return b.value - a.value;
            });
            console.log(bingbong)
            bongbing = bingbong[0].color 
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
	
	let promise = getColors();

	function handleClick() {
		promise = getColors();
	}

</script>


<h1 id="{bongbing}">
    colorAPI
</h1>

<input id="{bongbing}" bind:value="{searchTerm}" type="text"><button on:click="{handleClick}">check</button>

<p>
    find color in text quickly and easily
</p>

{#await promise then value}
	<p>the value is {value}</p>
    <p>{bongbing}</p>
    {#each bingbong as item}
    <p>
        {item.color} - {item.value}
    </p>   
    {/each}

{/await}

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