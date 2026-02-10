<script lang="ts">
	import '../app.css';
	import Hero from '$lib/components/Hero.svelte';
	import ChatMockup from '$lib/components/ChatMockup.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import { strings } from '$lib/strings';
	import { onMount } from 'svelte';

	const badMessages = [
		{ avatar: '/img/brad.png', name: strings['example.bad.message1.name'], timestamp: strings['example.bad.message1.timestamp'], body: strings['example.bad.message1.body'] },
		{ avatar: '/img/tim.png', name: strings['example.bad.reply1.name'], timestamp: strings['example.bad.reply1.timestamp'], body: strings['example.bad.reply1.body'] },
		{ avatar: '/img/brad.png', name: strings['example.bad.message2.name'], timestamp: strings['example.bad.message2.timestamp'], body: strings['example.bad.message2.body'] },
		{ avatar: '/img/tim.png', name: strings['example.bad.reply2.name'], timestamp: strings['example.bad.reply2.timestamp'], body: strings['example.bad.reply2.body'] },
	];

	const goodMessages = [
		{ avatar: '/img/sara.png', name: strings['example.good.message1.name'], timestamp: strings['example.good.message1.timestamp'], body: strings['example.good.message1.body'] },
		{ avatar: '/img/tim.png', name: strings['example.good.reply1.name'], timestamp: strings['example.good.reply1.timestamp'], body: strings['example.good.reply1.body'] },
		{ avatar: '/img/sara.png', name: strings['example.good.message2.name'], timestamp: strings['example.good.message2.timestamp'], body: strings['example.good.message2.body'] },
		{ avatar: '/img/tim.png', name: strings['example.good.reply2.name'], timestamp: strings['example.good.reply2.timestamp'], body: strings['example.good.reply2.body'] },
	];

	// easter egg: type three periods
	const easterEggCode = ['.', '.', '.'];
	let easterEggPos = 0;
	let overlayActive = $state(false);
	let preloaded = false;

	onMount(() => {
		function onKeydown(e: KeyboardEvent) {
			if (e.key === easterEggCode[easterEggPos]) {
				easterEggPos++;
				// preload image on second keypress
				if (easterEggPos === 2 && !preloaded) {
					const img = new Image();
					img.src = '/img/waiting.gif';
					preloaded = true;
				}
				if (easterEggPos === easterEggCode.length) {
					overlayActive = true;
					easterEggPos = 0;
				}
			} else {
				easterEggPos = 0;
			}
		}

		document.addEventListener('keydown', onKeydown);
		return () => document.removeEventListener('keydown', onKeydown);
	});

	function dismissOverlay() {
		overlayActive = false;
	}
</script>

<div id="wholesite">
	<Hero />

	<!-- Bad example -->
	<div class="container nonos">
		<div class="sections sectionleft">
			<h2 class="section-title">{strings['example.bad.title']}</h2>
			<ChatMockup messages={badMessages} cardClass="one" />
		</div>
		<div class="sections sectionright">
			<div class="list-card">
				<div>
					<p>{@html strings['example.bad.explanation.p1']}</p>
					<p>{@html strings['example.bad.explanation.p2']}</p>
					<p>{@html strings['example.bad.explanation.p3']}</p>
					<p>{@html strings['example.bad.explanation.p4']}</p>
				</div>
				<ul>
					{#each strings['example.bad.explanation.list'] as item}
						<li>{item}</li>
					{/each}
				</ul>
				<div>
					<p>{@html strings['example.bad.explanation.p5']}</p>
				</div>
			</div>
		</div>
	</div>

	<!-- Good example -->
	<div class="container yepyep">
		<div class="sections sectionleft">
			<h2 class="section-title">{strings['example.good.title']}</h2>
			<ChatMockup messages={goodMessages} cardClass="two" />
		</div>
		<div class="sections sectionright">
			<div class="list-card">
				<div>
					<p>{@html strings['example.good.explanation.p1']}</p>
					<p>{@html strings['example.good.explanation.p2']}</p>
					<p>{@html strings['example.good.explanation.p3']}</p>
				</div>
				<ul>
					{#each strings['example.good.explanation.list'] as item}
						<li>{item}</li>
					{/each}
				</ul>
				<div>
					<p>{@html strings['example.good.explanation.p4']}</p>
					<p>{@html strings['example.good.explanation.p5']}</p>
				</div>
			</div>
		</div>
	</div>

	<Footer />
</div>

<!-- Easter egg overlay -->
<!-- svelte-ignore a11y_click_events_have_key_events -->
<!-- svelte-ignore a11y_no_static_element_interactions -->
<div
	id="easter-egg-overlay"
	class:active={overlayActive}
	onclick={dismissOverlay}
	style="background-image: url('/img/waiting.gif');"
>
	<span class="overlay-text">...</span>
</div>
