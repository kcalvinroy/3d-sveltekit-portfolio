<script lang="ts">
	import { type Content, isFilled } from '@prismicio/client';
	import Bounded from '$lib/components/Bounded.svelte';
	import Heading from '$lib/components/Heading.svelte';
	import { PrismicRichText } from '@prismicio/svelte';
	import ContentList from './ContentList.svelte';

	export let slice: Content.ContentIndexSlice;

	export let items: Content.BlogpostDocument[] | Content.ProjectDocument[];
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<Heading size="xl" class="mb-8">
		{slice.primary.heading}
	</Heading>
	{#if isFilled.richText(slice.primary.description)}
		<div class="prose prose-xl prose-invert mb-10">
			<PrismicRichText field={slice.primary.description} />
		</div>
	{/if}

	<ContentList {items} viewMoreText={slice.primary.view_more_text} />
</Bounded>
