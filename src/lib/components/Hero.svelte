<script lang="ts">
	import { onMount } from 'svelte';
	import { strings, typedStrings } from '$lib/strings';

	let strikeEl: HTMLSpanElement;

	onMount(() => {
		let typed: InstanceType<typeof import('typed.js').default>;

		import('typed.js').then(({ default: Typed }) => {
			typed = new Typed(strikeEl, {
				strings: typedStrings,
				typeSpeed: 80,
				backSpeed: 60,
				smartBackspace: false,
				loop: true,
				shuffle: false,
				backDelay: 2000,
				startDelay: 3000,
			});

			// force cursor blink during startDelay
			if (typed.cursor != null) {
				typed.cursor.classList.add('typed-cursor--blink');
			}
		});

		return () => typed?.destroy();
	});
</script>

<div class="container">
	<div class="hero">
		<div>
			<h1 class="name">
				no <span id="strike" bind:this={strikeEl}></span>
			</h1>
		</div>
		<span class="subtitle">{strings['header.subtitle']}</span>
		<h2 class="lead">
			{strings['header.introduction']} {strings['header.emoji']}
		</h2>
	</div>
</div>
