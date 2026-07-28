<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import { page } from '$app/stores';
	import { gsap } from 'gsap';

	let { children } = $props();
	let menuOpen = $state(false);
	let contentWrapper: HTMLDivElement;

	// Toggle body class to prevent scrolling when menu is open
	$effect(() => {
		if (menuOpen) {
			document.body.classList.add('overflow-hidden');
		} else {
			document.body.classList.remove('overflow-hidden');
		}
	});

	// GSAP Animation for the content wrapper
	$effect(() => {
		if (menuOpen) {
			gsap.to(contentWrapper, {
				x: 280,
				scale: 0.82,
				borderRadius: '40px',
				borderColor: 'rgba(255, 255, 255, 0.12)',
				boxShadow: '-30px 30px 80px rgba(0, 0, 0, 0.8)',
				duration: 0.7,
				ease: 'back.out(1.4)',
				overwrite: true
			});
		} else {
			gsap.to(contentWrapper, {
				x: 0,
				scale: 1,
				borderRadius: '0px',
				borderColor: 'transparent',
				boxShadow: '0px 0px 0px rgba(0, 0, 0, 0)',
				duration: 0.5,
				ease: 'power2.inOut',
				overwrite: true
			});
		}
	});
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div
	class="relative min-h-screen w-full overflow-hidden bg-slate-950 font-sans text-white antialiased"
>
	<!-- Atmospheric Fog Effects (Root level) -->
	<div class="pointer-events-none fixed inset-0 z-0">
		<div
			class="absolute top-[10%] left-[10%] h-[40%] w-[40%] rounded-full bg-blue-500/10 blur-[120px]"
		></div>
		<div
			class="absolute top-[20%] right-[10%] h-[50%] w-[50%] rounded-full bg-purple-500/10 blur-[150px]"
		></div>
		<div
			class="absolute bottom-[20%] left-[20%] h-[60%] w-[60%] rounded-full bg-indigo-500/15 blur-[180px]"
		></div>

		<!-- Ground Fog -->
		<div
			class="absolute bottom-0 h-64 w-full bg-linear-to-t from-slate-950 via-slate-950/40 to-transparent backdrop-blur-[1px]"
		></div>
	</div>

	<!-- iOS-style Top Shadow/Gradient -->
	<div
		class="pointer-events-none fixed inset-x-0 top-0 z-40 h-32 bg-linear-to-b from-black/40 to-transparent"
	></div>

	<!-- Left Slide-out Menu -->
	<div
		class="fixed inset-y-0 left-0 z-20 flex w-[280px] flex-col justify-between p-6 transition-all duration-600 ease-[cubic-bezier(0.16,1,0.3,1)] select-none {menuOpen
			? 'pointer-events-auto opacity-100'
			: 'pointer-events-none opacity-0'}"
		style="transform: translateX({menuOpen ? '0' : '-40px'});"
	>
		<!-- Top: Profile Info & Navigation -->
		<div class="flex flex-col gap-8">
			<!-- Profile Card -->
			<div
				class="flex items-center gap-3 transition-all delay-75 duration-600"
				style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen ? '1' : '0'};"
			>
				<div
					class="relative flex h-12 w-12 items-center justify-center rounded-2xl bg-gradient-to-tr from-blue-500 to-purple-600 p-[2px] shadow-[0_0_20px_rgba(147,51,234,0.35)]"
				>
					<div
						class="flex h-full w-full items-center justify-center rounded-[14px] bg-slate-950 text-lg font-bold text-white"
					>
						S
					</div>
					<!-- Active pulse status -->
					<span class="absolute -right-0.5 -bottom-0.5 flex h-3.5 w-3.5">
						<span
							class="absolute inline-flex h-full w-full animate-ping rounded-full bg-emerald-400 opacity-75"
						></span>
						<span
							class="relative inline-flex h-3.5 w-3.5 rounded-full border border-slate-950 bg-emerald-500"
						></span>
					</span>
				</div>
				<div>
					<h3 class="text-sm font-bold tracking-wide text-white">SOTH</h3>
					<p class="text-[11px] text-white/50">Creative Developer</p>
				</div>
			</div>

			<!-- Nav Menu Links -->
			<div class="flex flex-col gap-1">
				<span
					class="px-3 pb-2 text-[10px] font-semibold tracking-widest text-white/30 uppercase transition-all delay-100 duration-600"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen ? '1' : '0'};"
				>
					Navigation
				</span>

				<a
					href="/"
					onclick={() => (menuOpen = false)}
					class="flex items-center gap-3.5 rounded-xl px-3 py-2.5 text-sm font-medium transition-all duration-300 hover:bg-white/5 hover:text-white {$page
						.url.pathname === '/'
						? 'bg-white/10 text-white'
						: 'text-white/60'}"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen
						? '1'
						: '0'}; transition-delay: 120ms;"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						width="18"
						height="18"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
						class="opacity-80"
						><path d="m3 9 9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z" /><polyline
							points="9 22 9 12 15 12 15 22"
						/></svg
					>
					<span>Home</span>
				</a>

				<a
					href="/about"
					onclick={() => (menuOpen = false)}
					class="flex items-center gap-3.5 rounded-xl px-3 py-2.5 text-sm font-medium transition-all duration-300 hover:bg-white/5 hover:text-white {$page
						.url.pathname === '/about'
						? 'bg-white/10 text-white'
						: 'text-white/60'}"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen
						? '1'
						: '0'}; transition-delay: 140ms;"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						width="18"
						height="18"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
						class="opacity-80"
						><path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2" /><circle
							cx="12"
							cy="7"
							r="4"
						/></svg
					>
					<span>About</span>
				</a>

				<a
					href="/my-projects"
					onclick={() => (menuOpen = false)}
					class="flex items-center gap-3.5 rounded-xl px-3 py-2.5 text-sm font-medium transition-all duration-300 hover:bg-white/5 hover:text-white {$page
						.url.pathname === '/my-projects'
						? 'bg-white/10 text-white'
						: 'text-white/60'}"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen
						? '1'
						: '0'}; transition-delay: 160ms;"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						width="18"
						height="18"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
						class="opacity-80"
						><path
							d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"
						/></svg
					>
					<span>Projects</span>
				</a>

				<a
					href="/my-skills"
					onclick={() => (menuOpen = false)}
					class="flex items-center gap-3.5 rounded-xl px-3 py-2.5 text-sm font-medium transition-all duration-300 hover:bg-white/5 hover:text-white {$page
						.url.pathname === '/my-skills'
						? 'bg-white/10 text-white'
						: 'text-white/60'}"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen
						? '1'
						: '0'}; transition-delay: 180ms;"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						width="18"
						height="18"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
						class="opacity-80"
						><path
							d="m12 3-1.912 5.886H3.82l4.912 3.57L6.82 18.342 12 14.772l5.18 3.57-1.912-5.886 4.912-3.57h-6.268z"
						/></svg
					>
					<span>Skills</span>
				</a>

				<a
					href="/contact"
					onclick={() => (menuOpen = false)}
					class="flex items-center gap-3.5 rounded-xl px-3 py-2.5 text-sm font-medium transition-all duration-300 hover:bg-white/5 hover:text-white {$page
						.url.pathname === '/contact'
						? 'bg-white/10 text-white'
						: 'text-white/60'}"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen
						? '1'
						: '0'}; transition-delay: 200ms;"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						width="18"
						height="18"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
						class="opacity-80"
						><rect width="20" height="16" x="2" y="4" rx="2" /><path
							d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"
						/></svg
					>
					<span>Contact</span>
				</a>
			</div>

			<!-- Connect Links -->
			<div class="flex flex-col gap-1">
				<span
					class="px-3 pb-2 text-[10px] font-semibold tracking-widest text-white/30 uppercase transition-all delay-220 duration-600"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen ? '1' : '0'};"
				>
					Connect
				</span>

				<a
					href="https://github.com"
					target="_blank"
					rel="noopener noreferrer"
					class="flex items-center gap-3.5 rounded-xl px-3 py-2 text-sm font-medium text-white/60 transition-all duration-300 hover:bg-white/5 hover:text-white"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen
						? '1'
						: '0'}; transition-delay: 240ms;"
				>
					<svg class="h-[18px] w-[18px]" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
						<path
							fill-rule="evenodd"
							d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.008.069-.008 1.003.07 1.53 1.032 1.53 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"
							clip-rule="evenodd"
						/>
					</svg>
					<span>GitHub</span>
				</a>

				<a
					href="https://linkedin.com"
					target="_blank"
					rel="noopener noreferrer"
					class="flex items-center gap-3.5 rounded-xl px-3 py-2 text-sm font-medium text-white/60 transition-all duration-300 hover:bg-white/5 hover:text-white"
					style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen
						? '1'
						: '0'}; transition-delay: 260ms;"
				>
					<svg class="h-[18px] w-[18px]" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
						<path
							fill-rule="evenodd"
							d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"
							clip-rule="evenodd"
						/>
					</svg>
					<span>LinkedIn</span>
				</a>
			</div>
		</div>

		<!-- Bottom: Resume CTA & Copyright -->
		<div class="flex flex-col gap-4">
			<a
				href="/resume.pdf"
				download
				class="flex items-center justify-center gap-2 rounded-xl border border-white/10 bg-white/5 py-3 text-sm font-semibold text-white transition-all duration-300 hover:scale-[1.02] hover:border-white/20 hover:bg-white/10 active:scale-[0.98]"
				style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen
					? '1'
					: '0'}; transition-delay: 280ms;"
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="15"
					height="15"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					stroke-width="2.5"
					stroke-linecap="round"
					stroke-linejoin="round"
					><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4" /><polyline
						points="7 10 12 15 17 10"
					/><line x1="12" y1="15" x2="12" y2="3" /></svg
				>
				<span>Download Resume</span>
			</a>

			<div
				class="text-center text-[10px] text-white/25 transition-all delay-300 duration-600"
				style="transform: translateY({menuOpen ? '0' : '20px'}); opacity: {menuOpen ? '1' : '0'};"
			>
				© 2026 SOTH • Portfolio v1.0
			</div>
		</div>
	</div>

	<!-- Backdrop/Overlay (behind wrapper when menu open to capture clicks on empty space and content) -->
	{#if menuOpen}
		<!-- svelte-ignore a11y_click_events_have_key_events -->
		<!-- svelte-ignore a11y_no_static_element_interactions -->
		<div
			onclick={() => (menuOpen = false)}
			class="fixed inset-0 z-10 cursor-pointer bg-black/20 backdrop-blur-[2px] transition-all duration-500"
		></div>
	{/if}

	<!-- Main Content Wrapper (Slides right and zooms out with smooth rounded corners) -->
	<div
		bind:this={contentWrapper}
		class="content-wrapper relative z-30 min-h-screen w-full border bg-slate-950 {menuOpen
			? 'pointer-events-none h-screen overflow-hidden'
			: ''}"
	>
		<!-- Header at the top -->
		<div
			class="relative z-40 flex justify-center p-4 transition-all duration-600 ease-[cubic-bezier(0.16,1,0.3,1)]"
			class:-translate-y-24={menuOpen}
			class:opacity-0={menuOpen}
			class:pointer-events-none={menuOpen}
		>
			<Header />
		</div>

		<!-- Main content -->
		<main class="relative z-20 w-full px-4 pt-4 pb-32">
			<div class="mx-auto max-w-6xl">
				{@render children()}
			</div>
		</main>
	</div>

	<!-- Footer navigation fixed at root level (stays fixed even during scroll/transform) -->
	<div
		class="fixed right-0 bottom-4 left-0 z-50 flex justify-center px-4 transition-all duration-600 ease-[cubic-bezier(0.16,1,0.3,1)]"
		class:translate-y-28={menuOpen}
		class:opacity-0={menuOpen}
		class:pointer-events-none={menuOpen}
	>
		<Footer {menuOpen} toggleMenu={() => (menuOpen = !menuOpen)} />
	</div>
</div>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		background-color: #020617; /* slate-950 */
	}

	.content-wrapper {
		transform-origin: left center;
		will-change: transform, border-radius;
	}
</style>
