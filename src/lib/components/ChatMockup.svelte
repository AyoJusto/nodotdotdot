<script lang="ts">
	type Message = {
		avatar: string;
		name: string;
		timestamp: string;
		body: string;
	};

	let {
		messages,
		cardClass = '',
	}: {
		messages: Message[];
		cardClass?: string;
	} = $props();
</script>

<div class="list-card example {cardClass}">
	{#each messages as msg}
		<div class="slack">
			<img src={msg.avatar} alt="{msg.name}'s avatar" />
			<span class="slackname">{msg.name}</span>
			<span class="slacktime">{msg.timestamp}</span><br />
			<span class="slackmessage">{msg.body}</span>
		</div>
	{/each}
</div>
