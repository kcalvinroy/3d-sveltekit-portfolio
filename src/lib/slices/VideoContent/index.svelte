<script lang="ts">
	import type { Content } from '@prismicio/client';
	import { PrismicEmbed } from '@prismicio/svelte';

	export let slice: Content.VideoContentSlice;
</script>

<PrismicEmbed
	field={slice.primary.video.html}
	class="not-prose w-full h-full rounded-md my-10 md:my-14 lg:my-16"
/>
