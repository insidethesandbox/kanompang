<script lang="ts">
	import { range } from 'es-toolkit';
	let mode = $state('fit-height');
    
    let pageAspect = 1;
    let innerHeight = $state(700);
    let innerWidth = $state(400);
    let pageHeight = $derived(Math.min(innerHeight, innerWidth))
    let pageWidth = $derived(pageHeight * pageAspect)

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

<div class="h-screen w-screen overflow-scroll">
	<div 
    style="
        height: {pageHeight}px;
        margin-top: {(innerHeight - pageHeight) / 2}px;
        margin-left: {(innerWidth - pageWidth) / 2}px;
    "
    class="flex">
		
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
