<script lang="ts">
	import clsx from 'clsx';
	export let tag = 'section';
</script>

<svelte:element
	this={tag}
	{...$$restProps}
	class={clsx('px-4 py-6 md:px-6 md:py-10 lg:py-14', $$props.class)}
>
	<div class="mx-auto w-full max-w-7xl"><slot /></div>
</svelte:element>
