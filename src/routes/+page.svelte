<script lang="ts">
	import { range } from 'es-toolkit';
	let mode = $state('fit-height');

	let pageAspect = 1;
	let innerHeight = $state(700);
	let innerWidth = $state(400);
	let pageHeight = $derived(Math.min(innerHeight, innerWidth));
	let pageWidth = $derived(pageHeight * pageAspect);

	const IMAGES = range(1, 23).map((i) => {
		const num = `00${i}`.slice(-3);
		return {
			page: i,
			src: `/book/page-${num}.jpeg`,
			pageCount: i === 1 || i === 22 ? 1 : 2
		};
	});
</script>

<svelte:window bind:innerHeight bind:innerWidth />

<div class="h-screen w-screen overflow-scroll bg-black">
	<div
		style="
        height: {pageHeight}px;
        margin-top: {(innerHeight - pageHeight) / 2}px;
        margin-left: {(innerWidth - pageWidth) / 2}px;
    "
		class="relative flex gap-4"
	>
		<a
			class="absolute bottom-0 left-0 rounded-tr-2xl bg-amber-100/90 px-4 py-2 hover:bg-amber-200/80"
			href="https://github.com/insidethesandbox/kanompang">View On Github</a
		>

		<a
			class="absolute top-0 left-0 rounded-br-2xl bg-amber-100/90 px-4 py-2 hover:bg-amber-200/80"
			href="https://drive.google.com/drive/folders/1Njb8Ij96BLg_7KX3r-ivzCsCUlh80Vlj?usp=drive_link"
		>
			Download PDF
		</a>

		<div class="absolute right-0 bottom-0 rounded-tl-2xl bg-amber-100/90 px-4 py-2">
			เลื่อนขวาเพื่อไปต่อ
			<!-- prettier-ignore -->
			<svg class="inline lucide lucide-chevron-right-icon lucide-chevron-right" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg>
		</div>
		{#each IMAGES as img}
			<img
				alt="page {img.page}"
				src={img.src}
				style="
                    aspect-ratio: ${img.pageCount};
                    max-width: none;
                    background-image: url({img.src})"
			/>
		{/each}
	</div>
</div>
