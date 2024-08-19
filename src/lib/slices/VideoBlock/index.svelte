<script lang="ts">
	import type { Content } from '@prismicio/client';
	import Bounded from '$lib/components/Bounded.svelte';
	import Heading from '$lib/components/Heading.svelte';

	export let slice: Content.VideoBlockSlice;

	let link: string = slice.primary.video_link.toString();
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<Heading tag="h2" size="sm">
		{slice.primary.video_label}
	</Heading>
	<Heading tag="h2" size="sm">
		{slice.primary.video_link}
	</Heading>
	<Heading tag="h2" size="sm">
		{link}
	</Heading>
	<div class="center">
		<iframe
			width="auto"
			height="auto"
			src={slice.primary.video_link}
			title={slice.primary.video_label}
			frameborder="0"
			allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
			referrerpolicy="origin"
			allowfullscreen
		></iframe>
	</div>
</Bounded>
