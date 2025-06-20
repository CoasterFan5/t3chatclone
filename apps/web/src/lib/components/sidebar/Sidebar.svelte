<script lang="ts">
	import Noise from '../Noise.svelte';
	import { getUserContext } from '$lib/context.svelte';
	import ThreadButton from './ThreadButton.svelte';
	import Searchbar from './Searchbar.svelte';

	const {
		username = 'Shadow User'
	}: {
		username?: string | null;
	} = $props();

	const ctx = getUserContext();

	let searchValue = $state('');
</script>

<nav class="sidebar">
	<h3 class="logo">CF CHAT</h3>
	<a href="/" class="createChat">
		<div class="createChatInnerWrap">
			<div class="createChatInner">Create Chat</div>
		</div>
	</a>
	<Searchbar bind:value={searchValue} />
	<div class="threads">
		{#each ctx.threadList as thread (thread.id)}
			{#if thread.name.toLowerCase().includes(searchValue.toLowerCase())}
				<ThreadButton name={thread.name} id={thread.id} currentThreadId={ctx.currentThreadId} />
			{/if}
		{/each}
	</div>
	<div class="accountInfoWrap">
		<div class="accountInfoInnerBorderBackground">
			<div class="accountInfoInnerBorder">
				<div class="accountInfoInner">
					<Noise color="var(--secondary)" />
					<span class="username"
						>{#if username}{username}{:else}Shadow User{/if}</span
					>
					<span class="usage">{ctx.messageLimit - ctx.messagesSent} Messages Remain</span>
				</div>
			</div>
		</div>
	</div>
</nav>

<style lang="scss">
	.sidebar {
		min-width: 15rem;
		width: 15rem;
		max-width: 15rem;
		background: var(--secondary);
		height: 100vh;
		padding: 1rem;
		display: flex;
		flex-direction: column;
		position: relative;
	}

	.logo {
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 1.5rem;
		margin: 0px;
		margin-bottom: 0.5rem;
		font-weight: 200;
	}

	.createChat {
		background: var(--background);
		opacity: 0.95;
		color: var(--text);
		text-align: center;
		width: 100%;
		text-decoration: none;
		border-radius: 0.5rem;
		font-size: 0.8rem;

		&:hover {
			opacity: 1;
			color: var(--primary);

			.createChatInnerWrap {
				background-image: linear-gradient(75deg, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.4));
			}
		}

		.createChatInnerWrap {
			background-image: linear-gradient(75deg, rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.3));
			padding: 1px;
			border-radius: 0.5rem;
			cursor: pointer;
			transition: all cubic-bezier(0.455, 0.03, 0.515, 0.955) 0.1s;

			.createChatInner {
				padding: 0.5rem;
				border-radius: calc(0.5rem - 1px);
				background: var(--background);
			}
		}
	}

	.threads {
		display: flex;
		flex-direction: column;
		align-items: start;
		justify-content: start;
		height: 100%;
		flex-grow: 1;
		gap: 0.25rem;
		margin-top: 1rem;
		overflow-y: auto;
		overflow-x: hidden;
	}

	.accountInfoWrap {
		position: absolute;
		bottom: 0px;
		left: 0px;
		width: 100%;
		padding: 1rem;
		display: flex;
		align-items: center;
		justify-content: center;

		.accountInfoInnerBorderBackground {
			width: 100%;
			height: 100%;
			background: var(--background);
			display: flex;
			border-radius: 0.25rem;
		}

		.accountInfoInnerBorder {
			background-image: linear-gradient(75deg, rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.3));
			border-radius: 0.25rem;
			width: 100%;
			height: 100%;
			padding: 1px;
		}

		.accountInfoInner {
			background: var(--background);
			border-radius: calc(0.25rem - 1px);
			padding: 0.5rem;
			display: flex;
			flex-direction: column;
			gap: 0.25rem;
			position: relative;

			.username {
				z-index: 1;
			}
			.usage {
				opacity: 0.7;
				z-index: 1;
				font-size: 0.75rem;
			}
		}
	}
</style>
