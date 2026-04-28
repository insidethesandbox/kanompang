<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import { MetaTags } from 'svelte-meta-tags';

	let { children } = $props();

	const title="ช่วงนี้น้องขนมปังไม่นุ่มฟู"
	const description="นิทานช่วยสื่อสารฟื้นฟูใจเด็กๆหลังเกิดภัยพิบัติ"
	const ogImage = 'kanompang.insidethesandbox.studio/book/page-001.jpeg'
</script>

<MetaTags
	{title}
	{description}
	openGraph={{
		title,
		description,
		images: [{ url: ogImage, alt: title }]
	}}
	twitter={{
		title,
		description,
		image: ogImage,
		imageAlt: title
	}}
/>
<svelte:head><link rel="icon" href={favicon} /></svelte:head>
{@render children()}
