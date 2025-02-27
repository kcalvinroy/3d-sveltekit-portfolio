<script lang="ts">
	import { SliceZone } from '@prismicio/svelte';
	import type { Content } from '@prismicio/client';

	import Bounded from './Bounded.svelte';
	import { formatDate } from '$lib/components/formatDate';
	import { components } from '$lib/slices';

	export let page: Content.BlogPostDocument | Content.ProjectDocument;

	const formattedDate = formatDate(page.data.date);
</script>

<Bounded tag="article">
	<div class="rounded-2xl border-2 border-slate-800 bg-slate-900 px-4 py-10 md:px-8 md:py-20">
		<!-- <Heading tag="h2">{page.data.title}</Heading> -->
		<h2
			class="flex flex-wrap font-bold text-3xl md:text-5xl leading-tight tracking-tight text-slate-300"
		>
			{page.data.title}
		</h2>
		<div class="pt-2 flex flex-wrap gap-4 text-yellow-400">
			{#each page.tags as tag}
				<span class="text-sm sm:text-base font-semibold">{tag}</span>
			{/each}
		</div>
		<p class="mt-8 border-b border-slate-600 text-xl font-medium text-slate-300">{formattedDate}</p>
		<div class="prose prose-lg prose-invert mt-12 w-full max-w-none md:mt-20">
			<SliceZone slices={page.data.slices} {components} />
		</div>
	</div>
</Bounded>
