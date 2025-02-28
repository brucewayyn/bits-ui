<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import type { Transition } from "$lib/internal/index.js";
	import type { ContentProps } from "../types.js";
	import { ctx } from "../ctx.js";

	type T = $$Generic<Transition>;
	type In = $$Generic<Transition>;
	type Out = $$Generic<Transition>;

	type $$Props = ContentProps<T, In, Out>;

	export let transition: $$Props["transition"] = undefined;
	export let transitionConfig: $$Props["transitionConfig"] = undefined;

	export let inTransition: $$Props["inTransition"] = undefined;
	export let inTransitionConfig: ContentProps<T>["inTransitionConfig"] = undefined;

	export let outTransition: $$Props["outTransition"] = undefined;
	export let outTransitionConfig: $$Props["outTransitionConfig"] = undefined;

	export let asChild = false;

	const { content, isSelected, props } = ctx.getContent();
</script>

{#if asChild && $isSelected(props)}
	{@const builder = $content(props)}
	<slot {builder} />
{:else if transition && $isSelected(props)}
	{@const builder = $content(props)}
	<div transition:transition={transitionConfig} use:melt={builder} {...$$restProps}>
		<slot {builder} />
	</div>
{:else if inTransition && outTransition && $isSelected(props)}
	{@const builder = $content(props)}
	<div
		in:inTransition={inTransitionConfig}
		out:outTransition={outTransitionConfig}
		use:melt={builder}
		{...$$restProps}
	>
		<slot {builder} />
	</div>
{:else if inTransition && $isSelected(props)}
	{@const builder = $content(props)}
	<div in:inTransition={inTransitionConfig} use:melt={builder} {...$$restProps}>
		<slot {builder} />
	</div>
{:else if outTransition && $isSelected(props)}
	{@const builder = $content(props)}
	<div out:outTransition={outTransitionConfig} use:melt={builder} {...$$restProps}>
		<slot {builder} />
	</div>
{:else if $isSelected(props)}
	{@const builder = $content(props)}
	<div {...$$restProps}>
		<slot {builder} />
	</div>
{/if}
