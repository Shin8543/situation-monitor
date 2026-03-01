<script lang="ts">
	import { isRefreshing, lastRefresh, autoRefreshInterval, refresh } from '$lib/stores';

	interface Props {
		onSettingsClick?: () => void;
		onRefreshClick?: () => void;
	}

	let { onSettingsClick, onRefreshClick }: Props = $props();

	const lastRefreshText = $derived(
		$lastRefresh
			? `最后更新: ${new Date($lastRefresh).toLocaleTimeString([], { hour: 'numeric', minute: '2-digit' })}`
			: '尚未刷新'
	);

	const intervals = [
		{ label: '1分钟', value: 60 * 1000 },
		{ label: '5分钟', value: 5 * 60 * 1000 },
		{ label: '15分钟', value: 15 * 60 * 1000 },
		{ label: '30分钟', value: 30 * 60 * 1000 },
		{ label: '1小时', value: 60 * 60 * 1000 }
	];

	function handleIntervalChange(event: Event) {
		const select = event.target as HTMLSelectElement;
		const value = parseInt(select.value);
		refresh.setAutoRefreshInterval(value, onRefreshClick);
	}
</script>

<header class="header">
	<div class="header-left">
		<h1 class="logo">态势监控系统</h1>
	</div>

	<div class="header-center">
		<div class="refresh-controls">
			<select
				class="interval-select"
				value={$autoRefreshInterval}
				onchange={handleIntervalChange}
				title="自动刷新间隔"
			>
				{#each intervals as interval}
					<option value={interval.value}>{interval.label}</option>
				{/each}
			</select>
			<button class="header-btn" onclick={onRefreshClick} disabled={$isRefreshing} title="立即刷新">
				<span class="btn-icon">↻</span>
				<span class="btn-label">刷新</span>
			</button>
			<div class="refresh-status">
				{#if $isRefreshing}
					<span class="status-text loading">刷新中...</span>
				{:else}
					<span class="status-text">{lastRefreshText}</span>
				{/if}
			</div>
		</div>
	</div>

	<div class="header-right">
		<button class="header-btn settings-btn" onclick={onSettingsClick} title="设置">
			<span class="btn-icon">⚙</span>
			<span class="btn-label">设置</span>
		</button>
	</div>
</header>

<style>
	.header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 0.5rem 1rem;
		background: var(--surface);
		border-bottom: 1px solid var(--border);
		position: sticky;
		top: 0;
		z-index: 100;
		gap: 1rem;
	}

	.header-left {
		display: flex;
		align-items: baseline;
		flex-shrink: 0;
	}

	.logo {
		font-size: 0.9rem;
		font-weight: 700;
		letter-spacing: 0.1em;
		color: var(--text-primary);
		margin: 0;
		display: flex;
		align-items: baseline;
		gap: 0.5rem;
	}

	.header-center {
		display: flex;
		align-items: center;
		flex: 1;
		justify-content: center;
		min-width: 0;
	}

	.refresh-controls {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		background: var(--surface);
		padding: 0.2rem 0.5rem;
		border-radius: 6px;
		border: 1px solid var(--border);
	}

	.interval-select {
		background: transparent;
		border: none;
		color: var(--text-secondary);
		font-size: 0.7rem;
		padding: 0.2rem 0.1rem;
		border-radius: 4px;
		cursor: pointer;
		outline: none;
	}

	.interval-select:hover {
		color: var(--text-primary);
	}

	.interval-select option {
		background: var(--surface);
		color: var(--text-primary);
	}

	.refresh-status {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		border-left: 1px solid var(--border);
		padding-left: 0.5rem;
	}

	.status-text {
		font-size: 0.6rem;
		color: var(--text-muted);
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}

	.status-text.loading {
		color: var(--accent);
	}

	.header-right {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		flex-shrink: 0;
	}

	.header-btn {
		display: flex;
		align-items: center;
		gap: 0.3rem;
		min-height: 2.75rem;
		padding: 0.4rem 0.75rem;
		background: transparent;
		border: 1px solid var(--border);
		border-radius: 4px;
		color: var(--text-secondary);
		cursor: pointer;
		transition: all 0.15s ease;
		font-size: 0.65rem;
	}

	.header-btn:hover {
		background: var(--border);
		color: var(--text-primary);
	}

	.btn-icon {
		font-size: 0.8rem;
	}

	.btn-label {
		display: none;
	}

	@media (min-width: 768px) {
		.btn-label {
			display: inline;
		}
	}
</style>
