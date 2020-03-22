<script>
	import { onMount } from 'svelte';

	const api = "https://coronavirus-19-api.herokuapp.com/countries/macedonia";
	let data = {};
	let virusImg = '/virus.svg';


	onMount(async () => {
		let results = await fetch(api);
		data = await results.json();
	});

	// Get the current date

	// Day in AL

	const dayWeeks = ['E Hënë', 'E Martë', 'E Mërkur', 'E Enjte', 'E Premte', 'E Shtunë', 'E Diel'];
	dayWeeks.reverse();
	


		var date = new Date();
		var result = date.toLocaleDateString("de", { // you can skip the first argument
		year: "numeric",
		month: "2-digit",
		day: "2-digit",
	});	

	var dayWeek = dayWeeks[date.getDay()];
		

	
</script>

<main>
<header>
	<div class="container">
		<img class="img-virus" src={virusImg} alt="virusIllustration">
		<h2 class="today py-2">{dayWeek + ' ' + result}</h2>
		<a href="tel:080000203" class="btn btn-danger header_btn">Telefono Urgjencën</a>
	</div>
</header>
	<div class="container">
	<h1 class="mt-5 text-center">Koronavirus ne Maqedoni</h1>
	<p class="text-center">Numrat e përgjithshëm të ndikimit që COVID-19 ka patur në Maqedoni deri tani.</p>
		<h2 class="text-center mt-5">Statitstika</h2>
		<div class="row">
			<div class="col-12 col-lg-4 mb-2">
				<div class="card shadow-sm text-center">
					<div class="card-body profile">
						<p  class="mb-0 lead subtitile">Raste</p>
						{#if data.cases === undefined}
						<h2 class="mb-0 ">Në ngarkim...</h2>
						{:else}
						<h2 class="mb-0">{data.cases}</h2>
						<i class="fa fa-plus-circle icon mt-2" aria-hidden="true"></i>
						{/if}

					</div>
				</div>
			</div>
			<div class="col-12 col-lg-4 mb-2">
				<div class="card shadow-sm text-center">
					<div class="card-body  profile">
						<p class="mb-0 lead">Të Shëruar</p>
						{#if data.cases === undefined}
						<h2 class="mb-0">Në ngarkim...</h2>
						{:else}
						<h2 class="mb-0 text-success">{data.recovered}</h2>
						<i class="fa fa-check-circle-o icon mt-2" aria-hidden="true"></i>

						{/if}
					</div>
				</div>
			</div>
			<div class="col-12 col-lg-4 mb-2">
				<div class="card shadow-sm text-center">
					<div class="card-body profile">
						<p class="mb-0 lead">Të vdekur</p>
						{#if data.cases === undefined}
						<h2 class="mb-0">Në ngarkim...</h2>
						{:else}
						<h2 class="mb-0 text-danger">{data.deaths}</h2>
						<i class="fa fa-heartbeat icon mt-2" aria-hidden="true"></i>

						{/if}
					</div>
				</div>
		</div>
	</div>
		<h2 class="mt-5">Sot</h2>
		<p>Numrat e fundit të ditës së sotme</p>
		<div class="row">
		<div class="col-12 col-lg-4 mb-2">
				<div class="card shadow-sm text-center">
					<div class="card-body profile">
						<p class="mb-0 lead">Raste të reja</p>
						{#if data.cases === undefined}
						<h2 class="mb-0">Në ngarkim...</h2>
						{:else}
						<h2 class="mb-0">{data.todayCases}</h2>
						{/if}
					</div>
				</div>
		</div>
			<div class="col-12 col-lg-4 mb-2">
			<div class="card shadow-sm text-center">
				<div class="card-body profile">
					<p class="mb-0 lead">Raste Kritike</p>
					{#if data.cases === undefined}
					<h2 class="mb-0">Në ngarkim...</h2>
					{:else}
					<h2 class="mb-0 text-danger">{data.critical}</h2>
					{/if}
				</div>
			</div>
		</div>
			<div class="col-12 col-lg-4 mb-2">
				<div class="card shadow-sm text-center">
					<div class="card-body profile">
						<p class="mb-0 lead">Raste Aktive</p>
						{#if data.cases === undefined}
						<h2 class="mb-0">Në ngarkim...</h2>
						{:else}
						<h2 class="mb-0">{data.active}</h2>
						{/if}
					</div>
				</div>
		</div>
		<footer>
			<div class="container">
				<p class="lead"> &copy; {date.getFullYear()}</p>
			</div>
		</footer>
</main>

<style>

	header {
		height: 50vh;
		background-color: #0d4991;
		position: relative;
	}

	.today {
		position: absolute;
		bottom: 50%;
		color: white;
	}

	.today-row {
		background-color: lightgrey;
	}

	.profile {
		border-bottom: 4px solid #0d4991;
		
	}

	.icon {
		color:darkgrey;
		font-size: 19px !important;
	}

	.img-virus {
		position: absolute;
		height:60%;
		opacity: .2;
		left: 50%;
		width: auto;
		top: 15%;
	}

	.header_btn {
		position: absolute;
		bottom:0;
		left:50%;
		transform: translate(-50%, 40%);
		font-size: 20px;
	}

	h2 {
		font-weight: bold;
	}

	@media screen and (max-width:576px) {
	
		.img-virus {
			position: relative;
			height: 150px;
			left: 50%;
			transform: translate(-50%, 50%);
			top: 70%;

		}

		.today {
			left: 50%;
    		top: 55%;
    		transform: translate(-50%, 50%);
   			 text-align: center;
		}
	}
</style>