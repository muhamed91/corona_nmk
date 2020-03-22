<script>

let selected;

    import { onMount } from 'svelte';
	const api = "https://coronavirus-19-api.herokuapp.com/countries";
	let data = [];
	let virusImg = '/virus.svg';


	onMount(async () => {
		let results = await fetch(api);
        data = await results.json();
        console.log(data);
    });
    
	

</script>


<main>
    <div class="container">
        <select class="form-control" bind:value={selected}>
  {#each data as cvalue}
    <option value={cvalue}>{cvalue.country}</option>
  {/each}
</select>

{#if selected}
    <div class="row">
        <div class="col-12 col-lg-4 mb-2">
        <div class="card shadow-sm text-center">
            <div class="card-body profile-cases">
                <p class="mb-0 lead">Raste</p>
                {#if selected.cases === undefined}
                <h2 class="mb-0">Në ngarkim...</h2>
                {:else}
                <h2 class="mb-0">{selected.cases}</h2>
               <i class="fa fa-plus-circle icon mt-2" aria-hidden="true"></i>
                {/if}
            </div>
        </div>
    </div>
     <div class="col-12 col-lg-4 mb-2">
        <div class="card shadow-sm text-center">
            <div class="card-body profile-rec">
                <p class="mb-0 lead">Të shëruar</p>
                {#if selected.recovered === undefined}
                <h2 class="mb-0">Në ngarkim...</h2>
                {:else}
                <h2 class="mb-0 text-success">{selected.recovered}</h2>
                <i class="fa fa-check-circle-o icon mt-2" aria-hidden="true"></i>
                {/if}
            </div>
        </div>
    </div>
     <div class="col-12 col-lg-4 mb-2">
        <div class="card shadow-sm text-center">
            <div class="card-body profile-death">
                <p class="mb-0 lead">Të vdekur</p>
                {#if selected.recovered === undefined}
                <h2 class="mb-0">Në ngarkim...</h2>
                {:else}
                <h2 class="mb-0 text-danger">{selected.deaths}</h2>
                <i class="fa fa-heartbeat icon mt-2" aria-hidden="true"></i>
                {/if}
            </div>
        </div>
    </div>
    </div>
{/if}


    </div>
</main>


<style>
 .icon {
		color:darkgrey;
		font-size: 19px !important;
	}

    .profile-cases {
        border-bottom: 4px solid black;
    }

    .profile-rec {
        border-bottom: 4px solid #28a745;
    }

    .profile-death {
        border-bottom: 4px solid #dc3545;
    }

    .form-control {
        font-size: 1.4rem !important;
    }

</style>