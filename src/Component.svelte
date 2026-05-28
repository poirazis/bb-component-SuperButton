<script>
  import { getContext } from "svelte";
  import { SuperButton } from "@poirazis/supercomponents-shared";

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  // Svelte 5 runes: ensure max-width: fit-content is always applied.
  // Guarded update prevents infinite loop when the store reacts to our own change.
  $effect(() => {
    const current = $component;
    if (!current?.styles) return;

    if (current.styles?.normal?.["max-width"] === "fit-content") return;

    component.update((c) => ({
      ...c,
      styles: {
        ...c.styles,
        normal: {
          ...c.styles?.normal,
          "max-width": "fit-content",
        },
      },
    }));
  });

  // Forward all props using runes ($$props still works due to compatibility mode)
  let props = $props();
</script>

<div use:styleable={$component.styles}>
  <SuperButton {...props} />
</div>
