<script lang="ts">
	import { type Content, isFilled } from '@prismicio/client';
	import Bounded from '$lib/components/Bounded.svelte';
	import Heading from '$lib/components/Heading.svelte';
	import { PrismicRichText } from '@prismicio/svelte';

	export let slice: Content.VideoBlockSlice;
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<div class="flex flex-col items-center relative pb-4 rounded-lg shadow-lg">
		<Heading size="sm" class="text-lg font-bold mb-2">{slice.primary.video_label}</Heading>
		<iframe
			class="relative max-w-full max-h-auto rounded-t-lg shadow-md"
			width="800"
			height="450"
			src={slice.primary.video_link}
			title={slice.primary.video_label}
			frameborder="0"
			allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
			referrerpolicy="origin"
			allowfullscreen
		></iframe>
		{#if isFilled.richText(slice.primary.video_description)}
			<p><PrismicRichText field={slice.primary.video_description} /></p>
		{/if}
	</div>
</Bounded>
