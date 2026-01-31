<script lang="ts">
	/**
	 * RelationshipManager - Foreign key relationship viewer
	 */
	interface Constraint {
		constraint_type: string;
		constraint_name: string;
		column_name?: string;
		foreign_table?: string;
		foreign_column?: string;
		definition?: string;
	}

	let {
		tableName,
		constraints = []
	}: {
		tableName: string;
		constraints: Constraint[];
	} = $props();

	const foreignKeys = $derived(constraints.filter(c => c.constraint_type === 'FOREIGN KEY'));
	const uniqueConstraints = $derived(constraints.filter(c => c.constraint_type === 'UNIQUE'));
	const checkConstraints = $derived(constraints.filter(c => c.constraint_type === 'CHECK'));
</script>

<div class="space-y-4">
	<div class="flex items-center gap-2">
		<h3 class="font-semibold">Relationships & Constraints</h3>
		<span class="badge badge-sm">{constraints.length}</span>
	</div>

	<div class="alert alert-info">
		<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
		</svg>
		<span class="text-sm">Viewing existing constraints. Full editor coming soon.</span>
	</div>

	{#if foreignKeys.length > 0}
		<div>
			<h4 class="text-xs uppercase font-bold opacity-50 mb-2">Foreign Keys ({foreignKeys.length})</h4>
			<div class="space-y-2">
				{#each foreignKeys as fk}
					<div class="p-3 bg-base-200 rounded-lg">
						<div class="font-mono text-sm font-bold">{fk.constraint_name}</div>
						{#if fk.definition}
							<div class="text-xs opacity-60 mt-1">{fk.definition}</div>
						{/if}
					</div>
				{/each}
			</div>
		</div>
	{/if}

	{#if uniqueConstraints.length > 0}
		<div>
			<h4 class="text-xs uppercase font-bold opacity-50 mb-2">Unique Constraints ({uniqueConstraints.length})</h4>
			<div class="space-y-2">
				{#each uniqueConstraints as uc}
					<div class="p-3 bg-base-200 rounded-lg">
						<div class="font-mono text-sm">{uc.constraint_name}</div>
					</div>
				{/each}
			</div>
		</div>
	{/if}

	{#if checkConstraints.length > 0}
		<div>
			<h4 class="text-xs uppercase font-bold opacity-50 mb-2">Check Constraints ({checkConstraints.length})</h4>
			<div class="space-y-2">
				{#each checkConstraints as cc}
					<div class="p-3 bg-base-200 rounded-lg">
						<div class="font-mono text-sm">{cc.constraint_name}</div>
						{#if cc.definition}<div class="text-xs opacity-60 mt-1">{cc.definition}</div>{/if}
					</div>
				{/each}
			</div>
		</div>
	{/if}

	{#if constraints.length === 0}
		<div class="text-center py-8 text-sm opacity-50">No constraints defined</div>
	{/if}
</div>
