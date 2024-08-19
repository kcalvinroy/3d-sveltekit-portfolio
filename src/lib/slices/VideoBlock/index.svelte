<script lang="ts">
	import type { Content } from '@prismicio/client';
	import Bounded from '$lib/components/Bounded.svelte';
	import Heading from '$lib/components/Heading.svelte';

	export let slice: Content.VideoBlockSlice;
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<div class="max-w-sm bg-white rounded-lg shadow-md">
		<iframe
			class="rounded-t-lg"
			width="800"
			height="450"
			src={slice.primary.video_link}
			title={slice.primary.video_label}
			frameborder="0"
			allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
			referrerpolicy="origin"
			allowfullscreen
		></iframe>
		<div class="flex items-center justify-between p-4">
			<h5 class="text-lg font-bold mb-2">{slice.primary.video_label}</h5>
			<p class="text-gray-600">{slice.primary.video_description}</p>
		</div>
	</div>
	<Heading tag="h2" size="sm">
		{slice.primary.video_label}
	</Heading>

	<div class="aspect-w-16 aspect-h-9">
		<iframe
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
</Bounded>
