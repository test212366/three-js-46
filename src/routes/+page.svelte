<script>
	import Lay from './$layout.svelte'
	import {fade} from 'svelte/transition'
	import gsap from 'gsap'
	import {SplitText} from 'gsap/SplitText'
 
	gsap.registerPlugin(SplitText)

	const customtransition = (node, {speed = 50}) => {
		let tl = gsap.timeline()
		let duration = 1000

		let chars = new SplitText(node, {type: "chars"})


		tl.from(chars.chars, {
			duration: duration / 1000,
			rotate: 90,
			opacity:0,
			y: 10,
			stagger: 0.1
		})
		const text = node.textContent
 
		return {
			duration,
			tick: t => {
				tl.progress(t)
			}
		}
	}
</script>


<style>
	:global(body) {
		position: relative;
		height: 100vh;
		overflow: hidden;
		width: 100vw;
	}
	:global(.content) {
		position: absolute;
		bottom: 100px;
		left: 100px;
	}
	:global(.nav) {
		position: fixed;
		top: 100px;
		right: 100px;
	}
</style>


<main class="content" transition:customtransition>
	<Lay />


	<h1> home</h1>
</main>
 
