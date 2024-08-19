<script lang="ts">
	import type { Content } from '@prismicio/client';
	import Bounded from '$lib/components/Bounded.svelte';
	import Heading from '$lib/components/Heading.svelte';
	import { PrismicRichText } from '@prismicio/svelte';

	export let slice: Content.VideoBlockSlice;
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<div class="max-w-sm bg-white rounded-lg shadow-md">
		<div class="relative pb-4/5">
			<iframe
				class="absolute w-full h-full rounded-t-lg"
				width="800"
				height="450"
				src={slice.primary.video_link}
				title={slice.primary.video_label}
				frameborder="0"
				allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
				referrerpolicy="origin"
				allowfullscreen
			></iframe>
		</div>
		<div class="p-4">
			<h3 class="text-lg font-bold mb-2">{slice.primary.video_label}</h3>
			<p class="text-gray-600">
				<PrismicRichText field={slice.primary.video_description} />
			</p>
		</div>
	</div>
</Bounded>
