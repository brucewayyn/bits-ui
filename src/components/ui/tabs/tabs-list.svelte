<script lang="ts">
	import { Tabs as TabsPrimitive } from "@/lib";
	import { cn } from "@/utils";

	type $$Props = TabsPrimitive.ListProps;

	let className: $$Props["class"] = undefined;
	export { className as class };
</script>

<TabsPrimitive.List
	class={cn(
		"inline-flex h-9 items-center justify-center rounded-lg bg-muted p-1 text-muted-foreground",
		className
	)}
	{...$$restProps}
>
	<slot />
</TabsPrimitive.List>
