<script lang="ts">
	import { asImageSrc, type Content } from '@prismicio/client';
	import { PrismicLink } from '@prismicio/svelte';
	import { gsap } from 'gsap';
	import type { Action } from 'svelte/action';
	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	export let items: Content.BlogpostDocument[] | Content.ProjectDocument[];

	$: contentImages = items.map((item) => {
		const image = item.data.hover_image;
		return asImageSrc(image, {
			fit: 'crop',
			w: 220,
			h: 320,
			exp: -10
		});
	});

	const onItemEnter: Action<HTMLElement, number> = (node, index) => {
		gsap.fromTo(
			node,
			{
				opacity: 0,
				y: 20
			},
			{
				opacity: 1,
				y: 0,
				duration: 1,
				ease: 'elastic.out(1,0.3)',
				stagger: 0.2,
				scrollTrigger: {
					trigger: node,
					start: 'top bottom-=100px',
					end: 'bottom center',
					toggleActions: 'play none none none'
				}
			}
		);

		const imageUrl = contentImages[index];
		if (imageUrl) {
			const img = new Image();
			img.src = imageUrl;
		}

		return {
			destroy() {}
		};
	};
</script>

<svelte:window />

<ul class="grid gap-6 sm:grid-cols-2 lg:grid-cols-3 border-b border-b-slate-100">
	{#each items as post, index (post.id + index)}
		<li class="relative group w-full opacity-100 pb-5" use:onItemEnter={index}>
			<PrismicLink
				document={post}
				class="flex flex-col justify-between backdrop-blur-[1] bg-white/5 shadow-lg rounded-xl p-6 h-full transition-transform duration-200 transform group-hover:scale-105 group-hover:shadow-2xl"
			>
				<div class="flex flex-col mb-4 flex-grow">
					<!-- Image section -->
					<img
						src={post.data.hover_image.url}
						alt={post.data.title}
						class="w-full h-48 object-cover rounded-t-lg"
					/>

					<span class="text-2xl font-semibold text-white/85 mt-4">{post.data.title}</span>
					<div class="flex flex-wrap gap-2 mt-2 text-yellow-400">
						{#each post.tags as tag}
							<span class="text-sm sm:text-base font-semibold">{tag}</span>
						{/each}
					</div>
				</div>
			</PrismicLink>
		</li>
	{/each}
</ul>
