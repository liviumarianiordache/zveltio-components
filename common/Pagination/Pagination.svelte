<script lang="ts">
	let {
		currentPage = 1,
		totalPages = 1,
		onPageChange
	}: {
		currentPage?: number;
		totalPages?: number;
		onPageChange: (page: number) => void;
	} = $props();

	const visiblePages = $derived(() => {
		const pages = [];
		const start = Math.max(1, currentPage - 2);
		const end = Math.min(totalPages, currentPage + 2);
		for (let i = start; i <= end; i++) pages.push(i);
		return pages;
	});
</script>

<div class="join">
	<button
		class="join-item btn btn-sm"
		disabled={currentPage === 1}
		onclick={() => onPageChange(currentPage - 1)}
	>«</button>
	
	{#each visiblePages() as page}
		<button
			class="join-item btn btn-sm {page === currentPage ? 'btn-active' : ''}"
			onclick={() => onPageChange(page)}
		>{page}</button>
	{/each}
	
	<button
		class="join-item btn btn-sm"
		disabled={currentPage === totalPages}
		onclick={() => onPageChange(currentPage + 1)}
	>»</button>
</div>
