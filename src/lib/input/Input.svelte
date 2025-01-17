<script lang="ts">
	import { createEventDispatcher } from "svelte";
	import type { HTMLInputAttributes } from "svelte/elements";

	const dispatch = createEventDispatcher();

	export let value: HTMLInputAttributes["value"] = "";
	export let type: HTMLInputAttributes["type"] = "text";
	export let placeholder: string = "";
	export let disabled: boolean = false;
	export let readonly: boolean = false;
	export let containerLabel: string = "";
	export let labelPlacement: "start" | "end" = "start";
	export let id: string | undefined = undefined;
	export let width: string | undefined = undefined;

	let inputRef: HTMLInputElement;

	export const focus = () => inputRef.focus();

	const change = (e: Event) => {
		value = (e.target as HTMLInputElement).value;
		dispatch("change", { value });
	};
</script>

<label for={id}><slot /></label>
<div
	style="width: {width ? width : ''};"
	aria-disabled={disabled}
	data-placement={labelPlacement}
	data-has-label={containerLabel.length > 0}
	class="flex place-items-center w-fit
    group aria-disabled:bg-gray-50 aria-disabled:dark:bg-gray-950 transition-all"
>
	{#if containerLabel}
		<span
			class="dark:bg-gray-950 bg-gray-50 font-light py-1 px-1 text-gray-300 dark:text-gray-500
			border-y border-gray-100 group-data-[placement='end']:order-2 dark:border-gray-900
			group-data-[placement='start']:rounded-l-md group-data-[placement='end']:rounded-r-md
			group-data-[placement='start']:border-l group-data-[placement='end']:border-r"
			>{containerLabel}</span
		>
	{/if}
	{#if type == "text"}
		<input
			{...$$restProps}
			{id}
			bind:this={inputRef}
			on:click
			on:keydown
			on:keyup
			on:input
			on:touchstart|passive
			on:touchend
			on:touchcancel
			on:mouseenter
			on:mouseleave
			bind:value
			type="text"
			{placeholder}
			autocomplete="off"
			class="bg-transparent outline-none px-2 py-1 border-gray-100 dark:border-gray-900 placeholder:text-gray-200
            flex-grow border group-data-[placement='start']:rounded-r-md group-data-[placement='end']:rounded-l-md
            group-data-[has-label=false]:rounded-md disabled:placeholder:text-gray-300 dark:placeholder:text-gray-600
          focus:border-gray-200 focus:dark:border-gray-800 disabled:hover:cursor-not-allowed transition-all
          disabled:dark:placeholder:text-gray-600 dark:text-gray-0 text-gray-999 min-w-0"
			{disabled}
			{readonly}
		/>
	{:else if type == "password"}
		<input
			{...$$restProps}
			{id}
			bind:this={inputRef}
			on:click
			on:keydown
			on:keyup
			on:input
			on:touchstart|passive
			on:touchend
			on:touchcancel
			on:mouseenter
			on:mouseleave
			bind:value
			type="password"
			{placeholder}
			{disabled}
			{readonly}
			autocomplete="off"
			class="bg-transparent outline-none px-2 py-1 border-gray-100 dark:border-gray-900 placeholder:text-gray-200
            flex-grow border group-data-[placement='start']:rounded-r-md group-data-[placement='end']:rounded-l-md
            group-data-[has-label=false]:rounded-md disabled:placeholder:text-gray-300 dark:placeholder:text-gray-600
          focus:border-gray-200 focus:dark:border-gray-800 disabled:hover:cursor-not-allowed transition-all
          disabled:dark:placeholder:text-gray-600 dark:text-gray-0 text-gray-999 min-w-0"
		/>
	{:else if type == "number"}
		<input
			{...$$restProps}
			{id}
			bind:this={inputRef}
			on:click
			on:keydown
			on:keyup
			on:input
			on:touchstart|passive
			on:touchend
			on:touchcancel
			on:mouseenter
			on:mouseleave
			bind:value
			type="number"
			{placeholder}
			{disabled}
			{readonly}
			class="bg-transparent outline-none px-2 py-1 border-gray-100 dark:border-gray-900 placeholder:text-gray-200
        flex-grow border group-data-[placement='start']:rounded-r-md group-data-[placement='end']:rounded-l-md
        group-data-[has-label=false]:rounded-md disabled:placeholder:text-gray-300 dark:placeholder:text-gray-600
      focus:border-gray-200 focus:dark:border-gray-800 disabled:hover:cursor-not-allowed transition-all
      disabled:dark:placeholder:text-gray-600 dark:text-gray-0 text-gray-999 dark:scheme-dark min-w-0"
		/>
	{:else}
		<input
			{...$$restProps}
			{id}
			bind:this={inputRef}
			on:click
			on:keydown
			on:keyup
			on:input
			on:touchstart|passive
			on:touchend
			on:touchcancel
			on:mouseenter
			on:mouseleave
			{value}
			{type}
			on:change={change}
			{placeholder}
			{disabled}
			{readonly}
			class="bg-transparent outline-none px-2 py-1 border-gray-100 dark:border-gray-900 placeholder:text-gray-200
            flex-grow border group-data-[placement='start']:rounded-r-md group-data-[placement='end']:rounded-l-md
            group-data-[has-label=false]:rounded-md disabled:placeholder:text-gray-300 dark:placeholder:text-gray-600
            focus:border-gray-200 focus:dark:border-gray-800 disabled:hover:cursor-not-allowed transition-all
            disabled:dark:placeholder:text-gray-600 dark:text-gray-0 text-gray-999 dark:scheme-dark min-w-0"
		/>
	{/if}
</div>

<style lang="postcss">
	@tailwind base;
	@tailwind components;
	@tailwind utilities;

	@layer utilities {
		.scheme-dark {
			color-scheme: dark;
		}
	}
</style>
