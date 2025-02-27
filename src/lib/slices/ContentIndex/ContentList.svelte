<script lang="ts">
	import {
		asImageSrc,
		isFilled,
		type Content,
		type ImageField,
		type KeyTextField
	} from '@prismicio/client';
	import { PrismicLink } from '@prismicio/svelte';
	import { gsap } from 'gsap';
	import type { Action } from 'svelte/action';
	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';

	import IconArrow from '~icons/ic/baseline-arrow-outward';

	gsap.registerPlugin(ScrollTrigger);

	export let items: Content.BlogpostDocument[] | Content.ProjectDocument[];
	export let fallbackItemImage: ImageField;
	export let viewMoreText: KeyTextField = 'Read More';

	let lastMousePos = { x: 0, y: 0 };
	let currentIndex: number | undefined;

	$: contentImages = items.map((item) => {
		const image = isFilled.image(item.data.hover_image) ? item.data.hover_image : fallbackItemImage;
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
				duration: 1.3,
				ease: 'elastic.out(1,0.3)',
				stagger: 0.2,
				scrollTrigger: {
					trigger: node,
					start: 'top bottom-=200px',
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

	const handleMouseMove = (e: MouseEvent) => {
		const mousePos = { x: e.clientX, y: e.clientY + window.scrollY };

		const speed = Math.sqrt(Math.pow(mousePos.x - lastMousePos.x, 2));

		const maxY = window.scrollY + window.innerHeight - 350;
		const maxX = window.innerWidth - 250;

		gsap.to('.hover-reveal', {
			x: gsap.utils.clamp(0, maxX, mousePos.x - 110),
			y: gsap.utils.clamp(0, maxY, mousePos.y - 160),
			rotation: speed * (mousePos.x > lastMousePos.x ? 1 : -1),
			ease: 'back.out(2)',
			duration: 1.3
		});

		gsap.to('.hover-reveal', {
			opacity: currentIndex === undefined ? 0 : 1,
			visibility: 'visible',
			ease: 'power3.out',
			duration: 0.6
		});

		lastMousePos = mousePos;
	};

	const onMouseEnter = (index: number) => {
		currentIndex = index;
	};

	const onMouseLeave = () => {
		currentIndex = undefined;
	};
</script>

<svelte:window on:mousemove={handleMouseMove} />

<ul
	on:mouseleave={onMouseLeave}
	class="grid gap-6 sm:grid-cols-2 lg:grid-cols-3 border-b border-b-slate-100"
>
	{#each items as post, index (post.id + index)}
		<li
			on:mouseenter={() => onMouseEnter(index)}
			class="relative group w-full opacity-100"
			use:onItemEnter={index}
		>
			<PrismicLink
				document={post}
				class="flex flex-col justify-between backdrop-blur-[1] bg-white/5 shadow-lg rounded-xl p-6 h-full transition-transform duration-300 transform group-hover:scale-105 group-hover:shadow-2xl"
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
