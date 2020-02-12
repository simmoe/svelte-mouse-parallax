<script>
	//https://github.com/wagerfield/parallax#11-installation
	import Parallax from 'parallax-js'

	import {slide} from 'svelte/transition'

	let images = 
	['https://image.flaticon.com/icons/svg/119/119596.svg',
	'https://image.flaticon.com/icons/svg/789/789395.svg',
	'https://image.flaticon.com/icons/svg/414/414927.svg',
	'https://image.flaticon.com/icons/svg/789/789392.svg']

	let scene, parallaxInstance

	const ready = node => {
		console.log(node)
		parallaxInstance = new Parallax(node)
		parallaxInstance.scalar(20.0)
		parallaxInstance.invert(false, false);
	}

	let showHappening = false
</script>

<main>
	<section>	
		<div use:ready class='container'>
			<!-- While all other options and parameters are optional, with sane defaults, and can be set programatically, each layer needs a data-depth attribute. The movement applied to each layer will be multiplied by its depth attribute. -->
			{#each images as image, index}
			<div data-depth='{index + .6}'>
				<img src='{image}' alt='' class='image{index}'/>
			</div>
			{/each}
		</div>
	</section>
	<section>
		<h3>Here's stuff</h3>
	</section>
	<div id='button' on:click={()=> showHappening = !showHappening}>click me</div>
	{#if showHappening}
		 <!-- content here -->
		<section in:slide out:slide id='happening'><h1>I am happening</h1></section>
	{/if}
</main>
<style>
	main{
		width:100vw;
		min-height:100vh;
		display:grid;
		place-items:center;
	}
	section{
		width:100vw;
		height:100vh;
		padding:20vh;
		display:grid;
		place-items:center;
		color:white;
	}
	#button{
		position:fixed;
		top:2rem;
		left:2rem;
		cursor:pointer;
		border:2px solid gray;
		color:gray;
		border-radius:1rem;
		padding:1rem;
		z-index:4;
	}
	#happening{
		position:fixed;
		top:0;
		left:0;
		background:rgba(255,255,255,.8);
		color:black;
	}
	section:nth-of-type(even){
		background:purple;
	}
	main img{
		width:40vw;
	}
	/* sun */
	.image1{
		width:10vw;
		margin: 2vw 0 0 16vw;
	}
	/* clouds */
	.image2{
		width:15vw;
		margin: 0 0 0 -100px;
	}
	/* birdie */
	.image3{
		width:20vw;
		margin: 40px 0 0 0;
	}
	:global(body, html) {
		margin:0;
		padding:0;
	}
	:global(*) {
		box-sizing:border-box;
	}

</style>