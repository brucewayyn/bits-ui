<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import { ctx } from "../ctx.js";
	import type { RadioGroupProps } from "../types.js";

	type $$Props = RadioGroupProps;
	export let value: $$Props["value"] = undefined;
	export let onValueChange: $$Props["onValueChange"] = undefined;
	export let asChild = false;

	const {
		elements: { radioGroup },
		states: { value: localValue }
	} = ctx.setRadioGroup({
		defaultValue: value,
		onValueChange: ({ next }) => {
			if (next) {
				onValueChange?.(next);
				value = next;
			}
			return next;
		}
	});

	$: value !== undefined && localValue.set(value);
</script>

{#if asChild}
	<slot builder={$radioGroup} />
{:else}
	{@const builder = $radioGroup}
	<div use:melt={builder} {...$$restProps}>
		<slot {builder} />
	</div>
{/if}
