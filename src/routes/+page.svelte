<script lang="ts">
	import { enhance } from '$app/forms';
	import { projects, profile } from '$lib/data';
	import ProjectRow from '$lib/components/ProjectRow.svelte';

	type Theme = 'light' | 'dark';
	type Status = 'idle' | 'loading' | 'success' | 'error';

	let theme: Theme = $state('light');
	let status: Status = $state('idle');
</script>

<div class="min-h-dvh bg-bg text-ink transition-colors duration-300 {theme === 'dark' ? 'dark' : ''}" style="background-color: var(--color-bg); color: var(--color-ink);">
	<!-- nav -->
	<header class="sticky top-0 z-50 backdrop-blur-md bg-bg/80 border-b border-line" style="border-color: var(--color-line);">
		<div
			class="mx-auto flex h-[60px] max-w-[1440px] items-center justify-between px-6 lg:h-[72px] lg:px-24"
		>
			<a href="/" class="text-[15px] font-semibold tracking-tight hover:opacity-85 transition-opacity lg:text-base">
				Portofolio Kei <span class="text-primary font-mono text-xs" style="color: var(--color-primary);">:p</span>
			</a>

			<div class="flex items-center gap-3 lg:gap-8">
				<nav class="hidden items-center gap-7 lg:flex">
					<a href="#proyek" class="text-sm text-muted hover:text-ink transition-colors" style="color: var(--color-muted);">Proyek</a>
					<a href="#tentang" class="text-sm text-muted hover:text-ink transition-colors" style="color: var(--color-muted);">Tentang</a>
					<a href="#kontak" class="text-sm text-muted hover:text-ink transition-colors" style="color: var(--color-muted);">Kontak</a>
				</nav>

				<!-- TOMBOL TEMA: Background diset putih/terang agar kontras -->
				<button
					type="button"
					aria-label="Ganti tema"
					onclick={() => (theme = theme === 'dark' ? 'light' : 'dark')}
					class="flex h-10 w-10 items-center justify-center rounded-xl border border-line hover:border-primary transition-all active:scale-95 lg:h-11 lg:w-11 shadow-sm"
					style="border-color: var(--color-line); background-color: {theme === 'dark' ? '#161615' : '#ffffff'};"
				>
					<svg
						width="17"
						height="17"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="1.5"
						stroke-linecap="round"
						stroke-linejoin="round"
						class="dark:hidden transition-transform hover:rotate-45"
					>
						<path d="M21 12.8A9 9 0 1 1 11.2 3a7 7 0 0 0 9.8 9.8Z" />
					</svg>
					<svg
						width="17"
						height="17"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="1.5"
						stroke-linecap="round"
						class="hidden dark:block transition-transform hover:rotate-90"
					>
						<circle cx="12" cy="12" r="4" />
						<path
							d="M12 2v2M12 20v2M4.9 4.9l1.4 1.4M17.7 17.7l1.4 1.4M2 12h2M20 12h2M4.9 19.1l1.4-1.4M17.7 6.3l1.4-1.4"
						/>
					</svg>
				</button>
			</div>
		</div>
	</header>

	<!-- hero -->
	<section class="mx-auto max-w-[1440px] px-6 pt-16 pb-14 lg:px-24 lg:pt-[120px]">
		<h1
			class="text-[52px] leading-[0.92] font-semibold tracking-[-2px] lg:text-[130px] lg:tracking-[-6px]"
			style="color: var(--color-ink);"
		>
			Keisha Putri Ratri
		</h1>

		<div class="mt-7 flex flex-col gap-6">
			<p class="max-w-[560px] text-[17px] leading-[1.6] text-muted lg:text-xl" style="color: var(--color-muted);">
				Siswa SMK jurusan RPL. Membangun antarmuka web yang cepat, rapi, dan mudah dipakai.
			</p>

			<div class="flex items-center gap-3">
				<a
					href="#proyek"
					class="flex h-12 items-center rounded-xl bg-primary px-6 text-[15px] font-medium text-on-primary shadow-sm hover:opacity-95 transition-all"
					style="background-color: var(--color-primary); color: var(--color-on-primary);"
				>
					Lihat proyek
				</a>
				<a
					href="#kontak"
					class="flex h-12 items-center rounded-xl border border-line px-6 text-[15px] transition-all"
					style="border-color: var(--color-line); color: var(--color-ink);"
				>
					Hubungi saya
				</a>
			</div>

			<p class="font-mono text-[11px] tracking-[1.1px] text-muted" style="color: var(--color-muted);">
				TERSEDIA UNTUK PROYEK BARU — 2026
			</p>
		</div>
	</section>

	<!-- band -->
	<div class="border-t border-line overflow-hidden" style="border-color: var(--color-line);">
		<img
			src={theme === 'dark' ? '/images/band-dark.png' : '/images/band-light.png'}
			alt="Foto kegiatan lab RPL"
			class="h-[220px] w-full object-cover lg:h-[420px]"
		/>
		<div class="mx-auto max-w-[1440px] px-6 py-4 lg:px-24">
			<p class="font-mono text-[11px] tracking-[1.1px] text-muted" style="color: var(--color-muted);">LAB RPL — SMK NEGERI 8 SEMARANG · 2026</p>
		</div>
	</div>

	<!-- proyek -->
	<section id="proyek" class="border-t border-line" style="border-color: var(--color-line);">
		<div class="mx-auto max-w-[1440px] px-6 pt-5 pb-14 lg:px-24 lg:pb-24">
			<p class="font-mono text-[11px] tracking-[1.1px]" style="color: var(--color-ink);">PROYEK</p>

			<div class="mt-7 flex flex-col divide-y divide-line lg:mt-10" style="border-color: var(--color-line);">
				{#each projects as project, i (project.title)}
					<ProjectRow {project} index={i} />
				{/each}
			</div>
		</div>
	</section>

	<!-- tentang -->
	<section id="tentang" class="border-t border-line" style="border-color: var(--color-line);">
		<div class="mx-auto max-w-[1440px] px-6 pt-5 pb-14 lg:px-24 lg:pb-24">
			<p class="font-mono text-[11px] tracking-[1.1px]" style="color: var(--color-ink);">TENTANG</p>

			<div class="mt-7 flex flex-col items-start gap-8 lg:mt-10 lg:flex-row lg:gap-24">
				<!-- FOTO PROFIL DENGAN GIF RASIO 4:5 -->
				<div class="aspect-[4/5] w-full lg:w-[420px] shrink-0 overflow-hidden rounded-2xl border shadow-sm" style="border-color: var(--color-line);">
					<img
						src="/images/Dance Dancing GIF.gif"
						alt="Dance Dancing"
						class="h-full w-full object-cover"
					/>
				</div>

				<div class="flex w-full flex-col gap-7">
					<p class="max-w-[520px] text-[17px] leading-[1.6] text-muted lg:text-xl" style="color: var(--color-muted);">
						{profile.bio}
					</p>

					<!-- KOTAK INFO TENTANG: Background diset putih/terang solid -->
					<div class="flex flex-col divide-y divide-line rounded-2xl border p-4 shadow-sm" style="background-color: {theme === 'dark' ? '#161615' : '#ffffff'}; border-color: var(--color-line);">
						{#each profile.facts as fact}
							<div class="flex items-center justify-between gap-8 py-3">
								<span class="font-mono text-[11px] tracking-[1.1px] text-muted" style="color: var(--color-muted);">
									{fact.label}
								</span>
								<span class="text-[15px]" style="color: var(--color-ink);">{fact.value}</span>
							</div>
						{/each}
					</div>

					<div class="flex flex-col gap-3">
						<span class="font-mono text-[11px] tracking-[1.1px] text-muted" style="color: var(--color-muted);">KEAHLIAN</span>
						<div class="flex flex-wrap gap-2">
							{#each profile.skills as skill}
								<!-- BADGE KEAHLIAN: Background diset putih/terang solid -->
								<span
									class="border px-3.5 py-1.5 rounded-xl font-mono text-[11px] tracking-[1.1px] shadow-sm"
									style="border-color: var(--color-line); background-color: {theme === 'dark' ? '#161615' : '#ffffff'}; color: var(--color-ink);"
								>
									{skill}
								</span>
							{/each}
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- kontak -->
	<section id="kontak" class="border-t border-line" style="border-color: var(--color-line);">
		<div class="mx-auto max-w-[1440px] px-6 pt-5 pb-14 lg:px-24 lg:pb-24">
			<p class="font-mono text-[11px] tracking-[1.1px]" style="color: var(--color-ink);">KONTAK</p>

			<div class="mt-7 flex flex-col gap-8 lg:mt-10 lg:flex-row lg:gap-24">
				<p class="max-w-[420px] text-[17px] leading-[1.6] text-muted lg:text-xl" style="color: var(--color-muted);">
					Punya pertanyaan atau ingin bekerja sama? Kirim pesan.
				</p>

				<!-- FORM KONTAK: Background diset putih/terang padat -->
				<form
					method="POST"
					action="?/kirim"
					use:enhance={() => {
						status = 'loading';
						return async ({ result, update }) => {
							await update({ reset: result.type === 'success' });
							status = result.type === 'success' ? 'success' : 'error';
						};
					}}
					class="flex w-full flex-col gap-4 lg:w-[440px] lg:shrink-0 p-6 rounded-2xl shadow-sm border"
					style="background-color: {theme === 'dark' ? '#161615' : '#ffffff'}; border-color: var(--color-line);"
				>
					<label class="flex flex-col gap-2">
						<span class="font-mono text-[11px] tracking-[1.1px]" style="color: var(--color-muted);">NAMA</span>
						<input
							name="nama"
							required
							autocomplete="name"
							placeholder="Nama lengkap kamu"
							class="h-12 w-full border px-3.5 text-[15px] outline-none rounded-xl transition-all"
							style="background-color: {theme === 'dark' ? '#0c0c0b' : '#fcfcfa'}; border-color: var(--color-line); color: var(--color-ink);"
						/>
					</label>

					<label class="flex flex-col gap-2">
						<span class="font-mono text-[11px] tracking-[1.1px]" style="color: var(--color-muted);">EMAIL</span>
						<input
							name="email"
							type="email"
							required
							autocomplete="email"
							placeholder="nama@email.com"
							class="h-12 w-full border px-3.5 text-[15px] outline-none rounded-xl transition-all"
							style="background-color: {theme === 'dark' ? '#0c0c0b' : '#fcfcfa'}; border-color: var(--color-line); color: var(--color-ink);"
						/>
					</label>

					<label class="flex flex-col gap-2">
						<span class="font-mono text-[11px] tracking-[1.1px]" style="color: var(--color-muted);">PESAN</span>
						<textarea
							name="pesan"
							required
							rows="5"
							placeholder="Tulis pesan kamu di sini"
							class="min-h-[120px] w-full border px-3.5 py-3 text-[15px] outline-none rounded-xl transition-all"
							style="background-color: {theme === 'dark' ? '#0c0c0b' : '#fcfcfa'}; border-color: var(--color-line); color: var(--color-ink);"
						></textarea>
					</label>

					<button
						type="submit"
						disabled={status === 'loading'}
						class="flex h-12 items-center justify-center gap-2 border px-6 text-[15px] font-medium rounded-xl transition-all"
						style={status === 'loading'
							? 'border-color: var(--color-line); background-color: var(--color-surface); color: var(--color-muted);'
							: 'background-color: var(--color-primary); color: var(--color-on-primary); border: none;'}
					>
						{#if status === 'loading'}
							<svg
								width="16"
								height="16"
								viewBox="0 0 24 24"
								fill="none"
								stroke="currentColor"
								stroke-width="1.5"
								stroke-linecap="round"
								class="animate-spin"
							>
								<path d="M12 3a9 9 0 1 0 9 9" />
							</svg>
							Mengirim...
						{:else}
							Kirim pesan
						{/if}
					</button>

					<!-- KOTAK STATUS -->
					{#if status !== 'idle'}
						<div class="flex items-center gap-3 border px-4 py-3.5 rounded-xl" style="background-color: {theme === 'dark' ? '#0c0c0b' : '#fcfcfa'}; border-color: var(--color-line);">
							{#if status === 'loading'}
								<svg
									width="16"
									height="16"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="1.5"
									stroke-linecap="round"
									class="animate-spin text-muted"
								>
									<path d="M12 3a9 9 0 1 0 9 9" />
								</svg>
								<span class="text-sm text-muted">Mengirim pesan...</span>
							{:else if status === 'success'}
								<svg
									width="16"
									height="16"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="1.5"
									stroke-linecap="round"
									stroke-linejoin="round"
									class="text-success"
								>
									<path d="M20 6 9 17l-5-5" />
								</svg>
								<span class="text-sm font-medium text-success">Pesan terkirim. Terima kasih!</span>
							{:else}
								<svg
									width="16"
									height="16"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="1.5"
									stroke-linecap="round"
									stroke-linejoin="round"
									class="text-danger"
								>
									<circle cx="12" cy="12" r="9" />
									<path d="M12 8v5M12 16.5v.01" />
								</svg>
								<span class="text-sm font-medium text-danger">Gagal mengirim. Coba lagi.</span>
							{/if}
						</div>
					{/if}
				</form>
			</div>
		</div>
	</section>

	<!-- footer -->
	<footer class="border-t border-line" style="border-color: var(--color-line);">
		<div class="mx-auto flex max-w-[1440px] flex-col gap-10 px-6 py-14 lg:px-24">
			<p
				class="max-w-[640px] text-[34px] leading-[1.05] font-medium tracking-[-0.6px] lg:text-[48px] lg:tracking-[-1.2px]"
				style="color: var(--color-ink);"
			>
				Mari membangun sesuatu.
			</p>

			<div
				class="flex flex-col items-start gap-4 lg:flex-row lg:items-center lg:justify-between lg:gap-6"
			>
				<a href="mailto:keishaputriratri@gmail.com" class="font-mono text-xs tracking-[1.1px] text-primary" style="color: var(--color-primary);">
					keishaputriratri@gmail.com
				</a>
				<div class="flex items-center gap-6">
					<a href="#proyek" class="font-mono text-[11px] tracking-[1.1px] text-muted" style="color: var(--color-muted);">PROYEK</a>
					<a
						href="https://github.com/kekukies"
						class="font-mono text-[11px] tracking-[1.1px] text-muted" style="color: var(--color-muted);">GITHUB</a
					>
					<a href="mailto:keishaputriratri@gmail.com" class="font-mono text-[11px] tracking-[1.1px] text-muted" style="color: var(--color-muted);">
						EMAIL
					</a>
				</div>
			</div>
		</div>
	</footer>
</div>