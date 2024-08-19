<script lang="ts">
	import type { Content } from '@prismicio/client';
	import Bounded from '$lib/components/Bounded.svelte';
	import Heading from '$lib/components/Heading.svelte';

	export let slice: Content.VideoBlockSlice;
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<div class="card">
		<iframe
			class="card-img"
			width="800"
			height="450"
			src={slice.primary.video_link}
			title={slice.primary.video_label}
			frameborder="0"
			allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
			referrerpolicy="origin"
			allowfullscreen
		></iframe>
		<h2 class="card-title">{slice.primary.video_label}</h2>
		<p class="card-text">{slice.primary.video_description}</p>
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
