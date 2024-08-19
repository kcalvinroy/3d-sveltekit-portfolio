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
	<div class="aspect-w-16 aspect-h-9">
		<iframe
			width="853"
			height="480"
			src="https://www.youtube.com/embed/9yIBuGwH2a0"
			title="Imagine Dragons - In Your Corner (Live) | Vevo Extended Play"
			frameborder="0"
			allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
			referrerpolicy="strict-origin-when-cross-origin"
			allowfullscreen
		></iframe>
	</div>
</Bounded>
