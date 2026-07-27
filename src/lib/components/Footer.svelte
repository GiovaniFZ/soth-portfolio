<script lang="ts">
	import { page } from '$app/stores';

	let { menuOpen = false, toggleMenu } = $props<{
		menuOpen?: boolean;
		toggleMenu?: () => void;
	}>();
</script>

<footer
	class="flex h-14 items-center justify-center gap-1.5 rounded-full border
                   border-white/10 bg-white/5
                   px-3 py-1 shadow-[0_8px_32px_rgba(0,0,0,0.4)]
                   backdrop-blur-3xl transition-all duration-300 hover:border-white/20 hover:shadow-[0_12px_40px_rgba(0,0,0,0.5)]
                   sm:gap-3 sm:px-5"
>
	<!-- Home Link -->
	<a
		href="/"
		class="group flex items-center gap-1.5 rounded-full px-3 py-1.5 text-xs font-semibold tracking-wide transition-all duration-300 hover:-translate-y-0.5 hover:scale-[1.03] active:scale-[0.97] sm:px-4 sm:text-sm {$page
			.url.pathname === '/'
			? 'bg-white/10 text-white shadow-[inset_0_1px_1px_rgba(255,255,255,0.1)]'
			: 'text-white/60 hover:bg-white/5 hover:text-white'}"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			width="16"
			height="16"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="transition-transform duration-300 group-hover:-translate-y-0.5 group-hover:scale-115"
		>
			<path d="m3 9 9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z" />
			<polyline points="9 22 9 12 15 12 15 22" />
		</svg>
		<span class="hidden min-[360px]:inline">Home</span>
	</a>

	<!-- About Link (Hidden on mobile, shown on tablet/desktop) -->
	<a
		href="/about"
		class="group hidden items-center gap-1.5 rounded-full px-4 py-1.5 text-sm font-semibold tracking-wide transition-all duration-300 hover:-translate-y-0.5 hover:scale-[1.03] active:scale-[0.97] sm:inline-flex {$page
			.url.pathname === '/about'
			? 'bg-white/10 text-white shadow-[inset_0_1px_1px_rgba(255,255,255,0.1)]'
			: 'text-white/60 hover:bg-white/5 hover:text-white'}"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			width="16"
			height="16"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="transition-transform duration-300 group-hover:-translate-y-0.5 group-hover:scale-115"
		>
			<path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2" />
			<circle cx="12" cy="7" r="4" />
		</svg>
		<span>About</span>
	</a>

	<!-- Projects Link -->
	<a
		href="/my-projects"
		class="group flex items-center gap-1.5 rounded-full px-3 py-1.5 text-xs font-semibold tracking-wide transition-all duration-300 hover:-translate-y-0.5 hover:scale-[1.03] active:scale-[0.97] sm:px-4 sm:text-sm {$page
			.url.pathname === '/my-projects'
			? 'bg-white/10 text-white shadow-[inset_0_1px_1px_rgba(255,255,255,0.1)]'
			: 'text-white/60 hover:bg-white/5 hover:text-white'}"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			width="16"
			height="16"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="transition-transform duration-300 group-hover:-translate-y-0.5 group-hover:scale-115"
		>
			<path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z" />
		</svg>
		<span class="hidden min-[360px]:inline">Projects</span>
	</a>

	<!-- Skills Link -->
	<a
		href="/my-skills"
		class="group flex items-center gap-1.5 rounded-full px-3 py-1.5 text-xs font-semibold tracking-wide transition-all duration-300 hover:-translate-y-0.5 hover:scale-[1.03] active:scale-[0.97] sm:px-4 sm:text-sm {$page
			.url.pathname === '/my-skills'
			? 'bg-white/10 text-white shadow-[inset_0_1px_1px_rgba(255,255,255,0.1)]'
			: 'text-white/60 hover:bg-white/5 hover:text-white'}"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			width="16"
			height="16"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="transition-transform duration-300 group-hover:-translate-y-0.5 group-hover:scale-115"
		>
			<path
				d="m12 3-1.912 5.886H3.82l4.912 3.57L6.82 18.342 12 14.772l5.18 3.57-1.912-5.886 4.912-3.57h-6.268z"
			/>
		</svg>
		<span class="hidden min-[360px]:inline">Skills</span>
	</a>

	<!-- Contact Link (Hidden on mobile, shown on tablet/desktop) -->
	<a
		href="/contact"
		class="group hidden items-center gap-1.5 rounded-full px-4 py-1.5 text-sm font-semibold tracking-wide transition-all duration-300 hover:-translate-y-0.5 hover:scale-[1.03] active:scale-[0.97] sm:inline-flex {$page
			.url.pathname === '/contact'
			? 'bg-white/10 text-white shadow-[inset_0_1px_1px_rgba(255,255,255,0.1)]'
			: 'text-white/60 hover:bg-white/5 hover:text-white'}"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			width="16"
			height="16"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="transition-transform duration-300 group-hover:-translate-y-0.5 group-hover:scale-115"
		>
			<rect width="20" height="16" x="2" y="4" rx="2" />
			<path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7" />
		</svg>
		<span>Contact</span>
	</a>

	<!-- "..." (More) Toggle Button -->
	<button
		onclick={toggleMenu}
		class="group flex cursor-pointer items-center justify-center rounded-full px-2.5 py-1.5 text-xs font-semibold transition-all duration-300 hover:-translate-y-0.5 hover:scale-[1.05] active:scale-[0.95] sm:px-3.5 sm:text-sm {menuOpen
			? 'bg-white/10 text-white shadow-[inset_0_1px_1px_rgba(255,255,255,0.15)]'
			: 'text-white/60 hover:bg-white/5 hover:text-white'}"
		aria-label="More options"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			width="18"
			height="18"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2.5"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="transition-transform duration-500 ease-out {menuOpen
				? 'rotate-90'
				: 'group-hover:scale-120 group-hover:rotate-180'}"
		>
			<circle cx="12" cy="12" r="1.2" />
			<circle cx="19" cy="12" r="1.2" />
			<circle cx="5" cy="12" r="1.2" />
		</svg>
	</button>
</footer>
