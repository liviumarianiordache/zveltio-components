<script lang="ts">
let {
    key,
    label,
    type = 'text',
    value = $bindable(),
    options = [],
    error = '',
    onLookupSearch = null
}: {
    key: string;
    label: string;
    type?: string;
    value?: any;
    options?: Array<{value: any; label: string}>;
    error?: string;
    onLookupSearch?: ((query: string) => Promise<any[]>) | null;
} = $props();
</script>

<div class="form-control">
    <label class="label"><span class="label-text">{label}</span></label>
    
    {#if type === 'text' || type === 'email' || type === 'number'}
        <input {type} bind:value class="input input-bordered {error ? 'input-error' : ''}" />
    {:else if type === 'textarea'}
        <textarea bind:value class="textarea textarea-bordered {error ? 'input-error' : ''}"></textarea>
    {:else if type === 'select'}
        <select bind:value class="select select-bordered {error ? 'input-error' : ''}">
            {#each options as opt}
                <option value={opt.value}>{opt.label}</option>
            {/each}
        </select>
    {:else if type === 'boolean'}
        <input type="checkbox" bind:checked={value} class="checkbox" />
    {/if}
    
    {#if error}<label class="label"><span class="label-text-alt text-error">{error}</span></label>{/if}
</div>