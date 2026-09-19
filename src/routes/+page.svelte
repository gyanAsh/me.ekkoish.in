<script>
	import { fly } from 'svelte/transition';
	import { cubicInOut } from 'svelte/easing';
	// 1. Declare reactive state using Svelte 5 Runes
	let visible = $state(false);

	// 2. $effect runs automatically when the component mounts in the browser
	$effect(() => {
		// Make it enter immediately on load
		visible = true;

		// Wait 3 seconds, then make it exit
		const timer = setTimeout(() => {
			visible = false;
		}, 3000);

		// The returned function automatically acts as the cleanup/unmount handler
		return () => clearTimeout(timer);
	});
	const filterId = `glass-${Math.random().toString(36).slice(2)}`;
	const time = new Date().toLocaleTimeString('en-US', {
		hour: 'numeric',
		minute: '2-digit',
		hour12: true
	});
</script>

<main class=" select-text">
	<section id="spotify" class="absolute top-25 left-10 z-1 -rotate-10 md:top-15">
		<iframe
			title="spotify"
			data-testid="embed-iframe"
			style="border-radius:12px"
			src="https://open.spotify.com/embed/playlist/72jlSysx3u2vAEaNOvreTS?utm_source=generator&theme=0&si=7c493c95931246d2"
			width="100%"
			height="352"
			frameborder="0"
			allowfullscreen
			allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
			loading="lazy"
		></iframe>
	</section>
</main>

<!-- Center wrapper -->
<section class=" absolute top-4 flex w-full items-center justify-center">
	<!-- Glass card -->
	{#if visible}
		<div
			in:fly={{ y: -200, duration: 800, easing: cubicInOut }}
			out:fly={{ y: -200, duration: 800, easing: cubicInOut }}
			class="relative z-9 max-w-sm grow overflow-hidden rounded-3xl border border-white/30 bg-white/20 shadow-2xl"
		>
			<!-- Glass layer: behind content, z-0 -->
			<div
				class="pointer-events-none absolute inset-0 z-0 backdrop-blur-lg"
				style={`backdrop-filter: url(#${filterId}) blur(0.5px); -webkit-backdrop-filter: url(#${filterId}) blur(10px);`}
			></div>

			<!-- Content: on top of glass, z-10 -->
			<div class="relative z-10 flex items-center gap-4 px-4 py-2 text-white select-none">
				<img src="./whatsapp.png" alt="whatsapp_logo" class="size-10 rounded-xl bg-[#25D366] p-2" />
				<div class="w-full text-slate-700">
					<div class="flex w-full items-center justify-between">
						<h2 class="text-base font-medium">Ashish</h2>
						<h2 class="text-sm font-medium">{time}</h2>
					</div>
					<p class=" text-sm font-medium">Let's go!!</p>
				</div>
			</div>
		</div>
	{/if}
</section>

<!-- SVG filter definition -->
<svg class="absolute h-0 w-0" aria-hidden="true">
	<defs>
		<filter
			id={filterId}
			x="-20%"
			y="-20%"
			width="140%"
			height="140%"
			color-interpolation-filters="sRGB"
		>
			<feTurbulence
				type="fractalNoise"
				baseFrequency="0.015"
				numOctaves="3"
				seed="2"
				result="noise"
			/>

			<feColorMatrix
				in="noise"
				type="matrix"
				values="0 0 0 0 0.5
                0 0 0 0 0.5
                0 0 0 0 1
                0 0 0 0 1"
				result="normal-map"
			/>

			<feDisplacementMap
				in="SourceGraphic"
				in2="normal-map"
				scale="30"
				xChannelSelector="R"
				yChannelSelector="G"
			/>
		</filter>
	</defs>
</svg>
