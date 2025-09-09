<script>
  import { getContext } from "svelte";
  import { SuperButton } from "@poirazis/supercomponents-shared";

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  $: $component.styles = {
    ...$component.styles,
    normal: {
      ...$component.styles.normal,
      flex: "none !important",
    },
  };
</script>

<div use:styleable={$component.styles}>
  <SuperButton {...$$props} />
</div>
