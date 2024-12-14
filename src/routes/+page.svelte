<script lang="ts">
	import SuperDebug, { superForm } from 'sveltekit-superforms';
	import type { PageData } from './$types';
	import { valibot } from 'sveltekit-superforms/adapters';
	import { schema } from './schema';
	import { Control, Description, Field, FieldErrors, Label } from 'formsnap';

	export let data: PageData;

	const form = superForm(data.form, {
		validators: valibot(schema)
	});

	const { form: formData, message, enhance, capture, restore } = form;

	export const snapshot = { capture, restore };
</script>

{#if $message}<h3>{$message}</h3>{/if}

<form method="POST" use:enhance>
	<Field {form} name="name">
		<Control>
			{#snippet children({ props })}
				<Label>Name</Label>
				<input {...props} type="test" bind:value={$formData.name} />
			{/snippet}
		</Control>
		<Description>Use your company email if you have one.</Description>
		<FieldErrors />
	</Field>

	<Field {form} name="email">
		<Control>
			{#snippet children({ props })}
				<Label>Email</Label>
				<input {...props} type="test" bind:value={$formData.email} />
			{/snippet}
		</Control>
		<Description>Use your company email if you have one.</Description>
		<FieldErrors />
	</Field>

	<div><button>Submit</button></div>
</form>

<hr />
<p>
	💥 <a target="_blank" href="https://superforms.rocks">Created with Superforms for SvelteKit</a> 💥
</p>
<SuperDebug data={$formData} />

<style>
	.invalid {
		color: red;
	}
</style>
