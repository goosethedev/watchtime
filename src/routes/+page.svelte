<script lang="ts">
  import IconBookmarkCircle from '@iconify-svelte/iconoir/bookmark-circle';
  import IconMovie from '@iconify-svelte/iconoir/cinema-old';
  import IconClockOutline from '@iconify-svelte/iconoir/clock-outline';
  import IconHistory from '@iconify-svelte/iconoir/clock-rotate-right';
  import IconFire from '@iconify-svelte/iconoir/fire-flame';
  import IconMoreVert from '@iconify-svelte/iconoir/more-vert';
  import IconNavArrowRight from '@iconify-svelte/iconoir/nav-arrow-right';
  import IconPlay from '@iconify-svelte/iconoir/play';
  import IconRefresh from '@iconify-svelte/iconoir/refresh';
  import IconSearch from '@iconify-svelte/iconoir/search';
  import IconSparks from '@iconify-svelte/iconoir/sparks';
  import IconStar from '@iconify-svelte/iconoir/star';
  import IconStarDashed from '@iconify-svelte/iconoir/star-dashed';
  import IconStatUp from '@iconify-svelte/iconoir/stat-up';
  import IconTrash from '@iconify-svelte/iconoir/trash';
  import IconTv from '@iconify-svelte/iconoir/tv';
  import IconXMark from '@iconify-svelte/iconoir/xmark';

  type IconComponent = typeof IconTv;
  type MediaType = 'show' | 'movie';
  type Filter = 'all' | 'shows' | 'movies';

  const getIcon: Record<MediaType, IconComponent> = {
    movie: IconMovie,
    show: IconTv,
  };

  interface QuickStat {
    label: string;
    value: string;
    icon: IconComponent;
    color: string;
  }

  interface ContinueWatchingItem {
    id: number;
    title: string;
    type: MediaType;
    subtitle: string;
    progress: number;
    gradient: string;
  }

  interface RecommendedItem {
    id: number;
    title: string;
    type: MediaType;
    year: number;
    genre: string;
    rating: number;
    reason: string;
    gradient: string;
  }

  interface WatchlistItem {
    id: number;
    title: string;
    type: MediaType;
    badge: string;
    gradient: string;
  }

  interface TrendingItem {
    id: number;
    rank: number;
    title: string;
    type: MediaType;
    gradient: string;
  }

  interface HistoryItem {
    id: number;
    title: string;
    subtitle: string;
    type: MediaType;
    watchedAgo: string;
    userRating: number;
    gradient: string;
  }

  // --- UI state ---------------------------------------------------
  let activeFilter: Filter = $state('all');

  function setFilter(filter: Filter) {
    activeFilter = filter;
  }

  // --- Placeholder data ---------------------------------------------------
  const quickStats: QuickStat[] = [
    { label: 'Shows Watched', value: '128', icon: IconTv, color: 'text-primary' },
    { label: 'Movies Watched', value: '342', icon: IconMovie, color: 'text-secondary' },
    { label: 'Hours Watched', value: '1,204', icon: IconClockOutline, color: 'text-accent' },
    { label: 'Day Streak', value: '18', icon: IconFire, color: 'text-warning' },
  ];

  const continueWatching: ContinueWatchingItem[] = [
    {
      id: 1,
      title: 'Severance',
      type: 'show',
      subtitle: 'S02E07 · "Chikhai Bardo"',
      progress: 68,
      gradient: 'from-indigo-600 to-purple-700',
    },
    {
      id: 2,
      title: 'Dune: Part Two',
      type: 'movie',
      subtitle: '54 min left',
      progress: 42,
      gradient: 'from-amber-600 to-orange-700',
    },
    {
      id: 3,
      title: 'The Bear',
      type: 'show',
      subtitle: 'S03E05 · "Children"',
      progress: 91,
      gradient: 'from-rose-600 to-red-700',
    },
    {
      id: 4,
      title: 'Oppenheimer',
      type: 'movie',
      subtitle: '1h 12m left',
      progress: 25,
      gradient: 'from-slate-600 to-slate-800',
    },
    {
      id: 5,
      title: 'Fallout',
      type: 'show',
      subtitle: 'S01E03 · "The Head"',
      progress: 55,
      gradient: 'from-emerald-600 to-teal-700',
    },
    {
      id: 6,
      title: 'The Last of Us',
      type: 'show',
      subtitle: 'S02E02 · "Through the Valley"',
      progress: 15,
      gradient: 'from-sky-600 to-blue-700',
    },
    {
      id: 7,
      title: 'Poor Things',
      type: 'movie',
      subtitle: '38 min left',
      progress: 78,
      gradient: 'from-fuchsia-600 to-pink-700',
    },
  ];

  const recommended: RecommendedItem[] = [
    {
      id: 11,
      title: 'Shōgun',
      type: 'show',
      year: 2024,
      genre: 'Drama',
      rating: 9.2,
      reason: 'Because you watched Slow Horses',
      gradient: 'from-indigo-600 to-purple-700',
    },
    {
      id: 12,
      title: 'Challengers',
      type: 'movie',
      year: 2024,
      genre: 'Drama',
      rating: 8.1,
      reason: 'Trending among people you follow',
      gradient: 'from-amber-600 to-orange-700',
    },
    {
      id: 13,
      title: 'Baby Reindeer',
      type: 'show',
      year: 2024,
      genre: 'Drama',
      rating: 8.6,
      reason: 'Because you watched Fleabag',
      gradient: 'from-rose-600 to-red-700',
    },
    {
      id: 14,
      title: 'Furiosa',
      type: 'movie',
      year: 2024,
      genre: 'Action',
      rating: 7.9,
      reason: 'Because you watched Mad Max',
      gradient: 'from-slate-600 to-slate-800',
    },
    {
      id: 15,
      title: 'Ripley',
      type: 'show',
      year: 2024,
      genre: 'Thriller',
      rating: 8.4,
      reason: 'Top pick for you',
      gradient: 'from-emerald-600 to-teal-700',
    },
    {
      id: 16,
      title: 'Civil War',
      type: 'movie',
      year: 2024,
      genre: 'Action',
      rating: 7.5,
      reason: 'Because you watched Ex Machina',
      gradient: 'from-sky-600 to-blue-700',
    },
  ];

  const watchlist: WatchlistItem[] = [
    {
      id: 21,
      title: 'The Penguin',
      type: 'show',
      badge: 'Releases Sep 2026',
      gradient: 'from-slate-600 to-slate-800',
    },
    {
      id: 22,
      title: 'Wicked: For Good',
      type: 'movie',
      badge: 'Releases Nov 2026',
      gradient: 'from-fuchsia-600 to-pink-700',
    },
    {
      id: 23,
      title: 'Alien: Earth',
      type: 'show',
      badge: 'Added 3 days ago',
      gradient: 'from-emerald-600 to-teal-700',
    },
    {
      id: 24,
      title: 'Blade Runner 2099',
      type: 'show',
      badge: 'Added 1 week ago',
      gradient: 'from-indigo-600 to-purple-700',
    },
    {
      id: 25,
      title: 'Gladiator II',
      type: 'movie',
      badge: 'Added 2 weeks ago',
      gradient: 'from-amber-600 to-orange-700',
    },
  ];

  const trending: TrendingItem[] = [
    {
      id: 31,
      rank: 1,
      title: 'House of the Dragon',
      gradient: 'from-rose-600 to-red-700',
      type: 'show',
    },
    {
      id: 32,
      rank: 2,
      title: 'Wednesday',
      gradient: 'from-slate-600 to-slate-800',
      type: 'movie',
    },
    {
      id: 33,
      rank: 3,
      title: 'Deadpool & Wolverine',
      gradient: 'from-amber-600 to-orange-700',
      type: 'movie',
    },
    {
      id: 34,
      rank: 4,
      title: 'Arcane',
      gradient: 'from-sky-600 to-blue-700',
      type: 'show',
    },
    {
      id: 35,
      rank: 5,
      title: 'Slow Horses',
      gradient: 'from-emerald-600 to-teal-700',
      type: 'show',
    },
  ];

  const history: HistoryItem[] = [
    {
      id: 41,
      title: 'Severance',
      subtitle: 'S02E06 · "Attila"',
      type: 'show',
      watchedAgo: '2 hours ago',
      userRating: 5,
      gradient: 'from-indigo-600 to-purple-700',
    },
    {
      id: 42,
      title: 'Dune: Part One',
      subtitle: 'Rewatch',
      type: 'movie',
      watchedAgo: 'Yesterday',
      userRating: 5,
      gradient: 'from-amber-600 to-orange-700',
    },
    {
      id: 43,
      title: 'The Bear',
      subtitle: 'S03E04 · "Violet"',
      watchedAgo: '2 days ago',
      type: 'movie',
      userRating: 4,
      gradient: 'from-rose-600 to-red-700',
    },
    {
      id: 44,
      title: 'Fallout',
      subtitle: 'S01E02 · "The Target"',
      type: 'movie',
      watchedAgo: '3 days ago',
      userRating: 4,
      gradient: 'from-emerald-600 to-teal-700',
    },
    {
      id: 45,
      title: 'Poor Things',
      subtitle: 'Movie',
      type: 'movie',
      watchedAgo: '5 days ago',
      userRating: 5,
      gradient: 'from-fuchsia-600 to-pink-700',
    },
  ];

  const filteredContinueWatching = $derived(
    activeFilter === 'all'
      ? continueWatching
      : continueWatching.filter((i) =>
          activeFilter === 'shows' ? i.type === 'show' : i.type === 'movie',
        ),
  );
</script>

<!--
  Reusable placeholder "poster" art.
  `Icon` is capitalised on purpose: in Svelte 5 a bare lowercase identifier used
  as a tag is treated as a literal HTML element, while a capitalised one (or a
  dotted member expression like `item.icon`) is treated as a dynamic component.
-->
{#snippet posterArt(gradient: string, Icon: IconComponent)}
  <div class="w-full h-full bg-linear-to-br {gradient} flex items-center justify-center">
    <Icon width="36" class="text-white/40" />
  </div>
{/snippet}

<div class="min-h-screen bg-base-200 pb-16">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-8">
    <!-- ===== Header ===== -->
    <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4 mb-6">
      <div class="flex items-center gap-3">
        <div class="avatar avatar-placeholder">
          <div class="bg-primary text-primary-content rounded-full w-14">
            <span class="text-xl">JD</span>
          </div>
        </div>
        <div>
          <h1 class="text-2xl font-bold">Welcome back, Jordan</h1>
          <p class="text-sm text-base-content/60">Here's what's happening in your watchlist</p>
        </div>
      </div>

      <div class="input input-bordered flex items-center gap-2 w-full sm:w-72">
        <IconSearch width="18" class="text-base-content/50" aria-hidden="true" />
        <label for="global-search" class="sr-only"> Search movies, shows, people... </label>
        <input
          id="global-search"
          type="text"
          class="grow"
          placeholder="Search movies, shows, people..."
        />
      </div>
    </div>

    <!-- ===== Stats + Weekly Goal ===== -->
    <div class="grid grid-cols-1 lg:grid-cols-4 gap-4 mb-10">
      <div class="stats stats-vertical sm:stats-horizontal lg:col-span-3 shadow bg-base-100">
        {#each quickStats as s}
          <div class="stat">
            <div class="stat-figure {s.color}">
              <s.icon width="26" />
            </div>
            <div class="stat-title">{s.label}</div>
            <div class="stat-value {s.color} text-2xl">{s.value}</div>
          </div>
        {/each}
      </div>

      <div class="card bg-base-100 shadow">
        <div class="card-body p-4 flex-row items-center justify-between">
          <div>
            <p class="text-xs text-base-content/60 mb-1">Weekly Goal</p>
            <p class="font-semibold text-sm">12 / 20 episodes</p>
          </div>
          <div
            class="radial-progress text-primary"
            style="--value:60; --size:3.5rem; --thickness:5px;"
            role="progressbar"
            aria-valuenow="60"
            aria-valuemin="0"
            aria-valuemax="100"
          >
            <span class="text-xs">60%</span>
          </div>
        </div>
      </div>
    </div>

    <!-- ===== Continue Watching ===== -->
    <section class="mb-10">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-lg font-bold flex items-center gap-2">
          <IconPlay width="22" class="text-primary" />
          Continue Watching
        </h2>
        <div role="tablist" class="tabs tabs-box tabs-sm">
          <button
            type="button"
            role="tab"
            class="tab {activeFilter === 'all' ? 'tab-active' : ''}"
            onclick={() => setFilter('all')}
          >
            All
          </button>
          <button
            type="button"
            role="tab"
            class="tab {activeFilter === 'shows' ? 'tab-active' : ''}"
            onclick={() => setFilter('shows')}
          >
            Shows
          </button>
          <button
            type="button"
            role="tab"
            class="tab {activeFilter === 'movies' ? 'tab-active' : ''}"
            onclick={() => setFilter('movies')}
          >
            Movies
          </button>
        </div>
      </div>

      <div class="carousel carousel-start gap-4 p-1 overflow-x-auto max-w-full">
        {#each filteredContinueWatching as item (item.id)}
          <div class="carousel-item">
            <div class="card bg-base-100 shadow-md hover:shadow-xl transition-shadow group">
              <figure class="relative h-24 sm:h-32 aspect-video overflow-hidden">
                {@render posterArt(item.gradient, getIcon[item.type])}
                <div
                  class="absolute inset-0 bg-black/0 group-hover:bg-black/40 transition-colors flex items-center justify-center"
                >
                  <button
                    type="button"
                    class="btn btn-circle btn-primary opacity-0 group-hover:opacity-100 transition-opacity"
                    aria-label="Resume"
                  >
                    <IconPlay width="22" />
                  </button>
                </div>
                <div class="absolute top-2 right-2 badge badge-neutral badge-sm gap-1">
                  {#if item.type === "movie"}
                    <IconMovie width="12" />
                    Movie
                  {:else}
                    <IconTv width="12" />
                    Show
                  {/if}
                </div>
                <progress
                  class="progress progress-primary absolute bottom-0 left-0 right-0 rounded-none h-1.5"
                  value={item.progress}
                  max="100"
                ></progress>
              </figure>
              <div class="card-body p-3">
                <h3 class="font-semibold text-sm truncate">{item.title}</h3>
                <p class="text-xs text-base-content/60 truncate">{item.subtitle}</p>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </section>

    <!-- ===== Recommended For You ===== -->
    <section class="mb-10">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-lg font-bold flex items-center gap-2">
          <IconSparks width="20" class="text-secondary" />
          Recommended For You
        </h2>
        <a href="/recommended" class="btn btn-ghost btn-sm gap-1">
          See all <IconNavArrowRight width="16" />
        </a>
      </div>

      <div class="carousel carousel-start gap-4 p-1 overflow-x-auto max-w-full">
        {#each recommended as item (item.id)}
          <div class="carousel-item">
            <div
              class="card w-40 sm:w-48 bg-base-100 shadow-md hover:shadow-xl transition-shadow group"
            >
              <figure class="relative h-56 sm:h-64 overflow-hidden">
                {@render posterArt(item.gradient, getIcon[item.type])}
                <div class="absolute top-2 left-2 badge badge-warning badge-sm gap-1">
                  <IconStar width="12" />
                  {item.rating}
                </div>
                <button
                  type="button"
                  class="btn btn-circle btn-xs btn-neutral absolute top-2 right-2 opacity-80 hover:opacity-100"
                  aria-label="Add to watchlist"
                >
                  <IconBookmarkCircle width="14" />
                </button>
              </figure>
              <div class="card-body p-3">
                <h3 class="font-semibold text-sm truncate">{item.title}</h3>
                <div class="flex items-center gap-1 text-xs text-base-content/60">
                  <span>{item.year}</span>
                  <span>·</span>
                  <span class="truncate">{item.genre}</span>
                </div>
                <p class="text-[11px] text-base-content/50 italic truncate">{item.reason}</p>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </section>

    <!-- ===== From Your Watchlist ===== -->
    <section class="mb-10">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-lg font-bold flex items-center gap-2">
          <IconBookmarkCircle width="20" class="text-accent" />
          From Your Watchlist
        </h2>
        <a href="/watchlist" class="btn btn-ghost btn-sm gap-1">
          See all <IconNavArrowRight width="16" />
        </a>
      </div>

      <div class="carousel carousel-start gap-4 p-1 overflow-x-auto max-w-full">
        {#each watchlist as item (item.id)}
          <div class="carousel-item">
            <div
              class="card w-40 sm:w-48 bg-base-100 shadow-md hover:shadow-xl transition-shadow group"
            >
              <figure class="relative h-56 sm:h-64 overflow-hidden">
                {@render posterArt(item.gradient, getIcon[item.type])}
                <button
                  type="button"
                  class="btn btn-circle btn-xs btn-neutral absolute top-2 right-2 opacity-80 hover:opacity-100"
                  aria-label="Remove from watchlist"
                >
                  <IconXMark width="14" />
                </button>
              </figure>
              <div class="card-body p-3">
                <h3 class="font-semibold text-sm truncate">{item.title}</h3>
                <div class="badge badge-ghost badge-sm">{item.badge}</div>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </section>

    <!-- ===== Trending This Week ===== -->
    <section class="mb-10">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-lg font-bold flex items-center gap-2">
          <IconStatUp width="20" class="text-error" />
          Trending This Week
        </h2>
        <a href="/trending" class="btn btn-ghost btn-sm gap-1">
          See all <IconNavArrowRight width="16" />
        </a>
      </div>

      <div class="carousel carousel-start gap-4 p-1 overflow-x-auto max-w-full">
        {#each trending as item (item.id)}
          <div class="carousel-item">
            <div class="card w-36 sm:w-44 bg-base-100 shadow-md hover:shadow-xl transition-shadow">
              <figure class="relative h-52 sm:h-60 overflow-hidden">
                {@render posterArt(item.gradient, getIcon[item.type])}
                <span
                  class="absolute -left-1 -bottom-3 text-6xl font-black text-white/20 leading-none select-none"
                >
                  {item.rank}
                </span>
              </figure>
              <div class="card-body p-3">
                <h3 class="font-semibold text-sm truncate">{item.title}</h3>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </section>

    <!-- ===== Recently Watched (History) ===== -->
    <section class="mb-10">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-lg font-bold flex items-center gap-2">
          <IconHistory width="20" class="text-info" />
          Recently Watched
        </h2>
        <a href="/history" class="btn btn-ghost btn-sm gap-1">
          Full history <IconNavArrowRight width="16" />
        </a>
      </div>

      <ul class="list bg-base-100 rounded-box shadow-md">
        {#each history as item (item.id)}
          <li class="list-row items-center">
            <div class="w-12 h-12 rounded-lg overflow-hidden shrink-0">
              {@render posterArt(item.gradient, getIcon[item.type])}
            </div>
            <div class="list-col-grow">
              <div class="font-medium text-sm">{item.title}</div>
              <div class="text-xs text-base-content/60">{item.subtitle}</div>
            </div>
            <div class="hidden sm:flex items-center gap-0.5 text-warning">
              {#each Array(5) as _, i}
                {#if i < item.userRating}
                  <IconStar width="12" />
                {:else}
                  <IconStarDashed width="12" />
                {/if}
              {/each}
            </div>
            <div class="text-xs text-base-content/50 whitespace-nowrap">{item.watchedAgo}</div>
            <div class="dropdown dropdown-end">
              <button
                type="button"
                class="btn btn-ghost btn-square btn-sm"
                aria-label="More options"
              >
                <IconMoreVert width="16" />
              </button>
              <ul class="dropdown-content menu bg-base-100 rounded-box shadow-lg w-44 z-10 mt-2">
                <li>
                  <button type="button"><IconRefresh width="14" /> Rewatch</button>
                </li>
                <li>
                  <button type="button"><IconStarDashed width="14" /> Rate</button>
                </li>
                <li>
                  <button type="button" class="text-error">
                    <IconTrash width="14" />
                    Remove
                  </button>
                </li>
              </ul>
            </div>
          </li>
        {/each}
      </ul>
    </section>
  </div>
</div>
