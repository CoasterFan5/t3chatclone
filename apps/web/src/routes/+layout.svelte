<script lang="ts">
	import Toaster from '$lib/components/toaster/Toaster.svelte';
	import '$lib/global.scss';
	const { children } = $props();
</script>

<Toaster />
{@render children?.()}

<style lang="scss">
	// A very creative color palette
	:global(body) {
		--background: #1b1b1b;
		--text: #f1f1f1;
		--text-50: color-mix(in srgb, var(--text) 50%, transparent 50%);
		--primary: #ff7518;

		--primary-10: color-mix(in srgb, var(--primary) 10%, transparent 90%);
		--secondary: #2f2f2f;

		background: var(--background);
		color: var(--text);
	}
</style>
