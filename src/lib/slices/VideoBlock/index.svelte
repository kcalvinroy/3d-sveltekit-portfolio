<script lang="ts">
	import type { Content } from '@prismicio/client';

	export let slice: Content.VideoBlockSlice;
</script>

<section data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	Placeholder component for {slice.slice_type} (variation: {slice.variation}) Slices
	<embed
		src={slice.primary.video_link}
		title={slice.primary.video_label}
		allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
		allowfullscreen
		class="w-full h-full"
	/>
</section>
