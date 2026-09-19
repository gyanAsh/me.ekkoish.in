<script lang="ts">
	import './layout.css';

	const { children } = $props();
</script>

<div class="relative max-h-dvh min-h-dvh max-w-dvw min-w-dvw bg-[#5595fc]">
	<div
		class="mask-from-black mask-from-50% mask-to-transparent mask-to-100% absolute top-0 right-0 bottom-0 left-0 bg-[linear-gradient(to_right,#ffffff33_1px,transparent_1px),linear-gradient(to_bottom,#ffffff33_1px,transparent_1px)] mask-radial-[ellipse_80%_40%_at_38%_30%] bg-size-[3.5rem_3.5rem]"
	></div>
	<div
		class="absolute top-0 right-0 bottom-0 left-0 bg-radial-[140%_125%_at_50%_10%] from-[rgba(255,255,255,0.3)] from-40% to-[rgba(250,250,250,1)] to-100%"
	></div>
	{@render children()}
</div>
