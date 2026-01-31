<script lang="ts">
	/**
	 * MetadataSettings - Table metadata editor (display name, menu group, audit)
	 */
	interface Metadata {
		displayName?: string;
		menuGroup?: string;
		isLoggable?: boolean;
		icon?: string;
	}

	let {
		metadata = $bindable<Metadata>({})
	}: {
		metadata?: Metadata;
	} = $props();
</script>

<div class="space-y-4 p-4 bg-base-200 rounded-lg">
	<h4 class="font-semibold">Table Metadata</h4>
	
	<div class="form-control">
		<label class="label"><span class="label-text-alt">Display Name</span></label>
		<input
			type="text"
			bind:value={metadata.displayName}
			placeholder="User Profiles"
			class="input input-sm input-bordered"
		/>
	</div>

	<div class="form-control">
		<label class="label"><span class="label-text-alt">Menu Group</span></label>
		<input
			type="text"
			bind:value={metadata.menuGroup}
			placeholder="Administration"
			class="input input-sm input-bordered"
		/>
	</div>

	<div class="form-control">
		<label class="label"><span class="label-text-alt">Icon</span></label>
		<input
			type="text"
			bind:value={metadata.icon}
			placeholder="Users"
			class="input input-sm input-bordered"
		/>
	</div>

	<div class="form-control">
		<label class="label cursor-pointer justify-start gap-2">
			<input
				type="checkbox"
				bind:checked={metadata.isLoggable}
				class="toggle toggle-sm toggle-primary"
			/>
			<span class="label-text">Enable Audit Log</span>
		</label>
	</div>
</div>
