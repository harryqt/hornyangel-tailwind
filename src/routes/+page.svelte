<script>
	import { FontAwesomeIcon } from '@fortawesome/svelte-fontawesome';
	import {
		faMagnifyingGlass,
		faBars,
		faFire,
		faUsers,
		faWandMagicSparkles,
		faClock,
		faCircleCheck,
		faPhotoFilm,
		faShieldHeart
	} from '@fortawesome/free-solid-svg-icons';
	import { faCircleDot } from '@fortawesome/free-regular-svg-icons';
	import { config } from '@fortawesome/fontawesome-svg-core';
	import asideData from '$lib/aside-data.json';

	import '@fortawesome/fontawesome-svg-core/styles.css'; // Import the CSS
	config.autoAddCss = false; // Tell Font Awesome to skip adding the CSS automatically since it's being imported above

	const iconMap = {
		Trending: {
			icon: faFire,
			classes: 'flex items-center gap-2 rounded-lg border border-red-400 px-3 py-1.5'
		},
		Models: {
			icon: faUsers,
			classes: 'flex items-center gap-2 px-3 py-0.5'
		},
		'Live Sex': {
			icon: faCircleDot,
			classes: 'flex items-center gap-2 px-3 py-0.5 text-red-600',
			props: { fade: true }
		}
	};

	const filters = [
		{ icon: faWandMagicSparkles, label: 'Recommended' },
		{ icon: faClock, label: 'Under 10 min' },
		{ icon: faCircleCheck, label: 'Verified' },
		{ icon: faPhotoFilm, label: '4K' },
		{ icon: faShieldHeart, label: 'Safe Search' }
	];

	const paragraphs = [
		'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
		'Praesent tempor nisl eu justo dapibus, at scelerisque lectus viverra.',
		'Donec vestibulum in augue eget euismod Ut consequat fringilla augue in luctus.',
		'Praesent purus felis, sodales vitae erat sit amet, laoreet iaculis urna.',
		'Cras sit amet sapien a turpis lobortis cursus id id velit.',
		'Etiam luctus quis diam a accumsan. Nullam fermentum gravida ante, sed placerat quam.',
		'Ut lobortis felis nec felis imperdiet porttitor. Suspendisse non felis vehicula, luctus velit eget, mollis mi.'
	];

	let showAside = $state(false);
</script>

<nav
	class="sticky top-0 flex items-center justify-between border border-b-slate-700 bg-linear-to-b from-slate-800 to-stone-950 px-4 py-3"
>
	<!-- Left: Logo + Brand -->
	<a href="/" class="flex items-center gap-2">
		<img src="/img/logo.png" alt="HornyAngel logo" class="h-6 w-6" />
		<span class="text-base font-bold text-slate-100">HornyAngel.Org</span>
	</a>

	<!-- Right: Actions -->
	<div class="flex items-center gap-2">
		<button>
			<FontAwesomeIcon
				class="rounded-xl border border-slate-700 bg-slate-800 p-3 text-xs text-slate-100"
				icon={faMagnifyingGlass}
			/>
		</button>
		<button onclick={() => (showAside = !showAside)} class="cursor-pointer">
			<FontAwesomeIcon
				class="rounded-xl border border-slate-700 bg-slate-800 p-3 text-xs text-slate-100"
				icon={faBars}
			/>
		</button>
	</div>
</nav>

<!-- svelte-ignore a11y_invalid_attribute -->
<aside
	class="fixed h-full w-64 -translate-x-full transform overflow-y-auto bg-gray-900 p-5 transition-transform duration-200 ease-in-out"
	class:translate-x-0={showAside}
>
	{#each asideData as section}
		{#if section.type === 'Browse'}
			<section class="pb-3">
				<div class="pb-3 text-xs tracking-widest text-slate-400 uppercase">{section.type}</div>
				<nav class="flex flex-col gap-2 text-slate-100">
					{#each section.items as item}
						<a href="#" class={iconMap[item]?.classes ?? ''}>
							{#if iconMap[item]}
								<FontAwesomeIcon icon={iconMap[item].icon} {...iconMap[item].props ?? {}} />
							{/if}
							{item}
						</a>
					{/each}
				</nav>
			</section>
		{:else}
			<section class="pb-3 last:pb-24">
				<div class="pb-3 text-xs tracking-widest text-slate-400 uppercase">{section.type}</div>
				<nav class="ml-6 flex flex-col gap-3 text-slate-100">
					{#each section.items as item}
						<a href="#">{item}</a>
					{/each}
				</nav>
			</section>
		{/if}
	{/each}
</aside>

<!-- svelte-ignore a11y_invalid_attribute -->
<main class="min-h-screen bg-gray-950">
	<div class="flex flex-wrap gap-3 p-6 text-sm text-slate-100">
		{#each filters as { icon, label }}
			<a class="flex items-center gap-2 rounded-3xl border border-slate-700 px-3 py-1.5" href="#">
				<FontAwesomeIcon {icon} />
				{label}
			</a>
		{/each}
	</div>

	<div class="flex items-center justify-between px-5 pb-6">
		<p class="text-slate-400">59 Videos</p>
		<select class="rounded-xl border border-slate-700 bg-slate-800 text-sm text-slate-100">
			<option value="trending" selected="">Sort: Trending</option>
			<option value="newest">Newest</option>
			<option value="most_viewed">Most Viewed</option>
			<option value="top_rated">Top Rated</option>
		</select>
	</div>

	<div class="grid grid-cols-1 place-items-center gap-6">
		{#each paragraphs as text}
			<div class="h-48 w-80 overflow-hidden rounded-xl bg-amber-100">
				<div class="h-32 w-full bg-slate-400"></div>
				<p class="p-2 text-sm text-slate-800">{text}</p>
			</div>
		{/each}
	</div>
</main>
