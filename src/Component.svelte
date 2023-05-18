<script>
  import { getContext } from "svelte"

  const { styleable } = getContext("sdk")
  const component = getContext("component")
  const buttonGroupStore = getContext("super-action-button-group")

  export let size
  export let icon
  export let text
  export let emphasized
  export let quiet
  export let selected
  export let disabled
  export let onClick

  function handleClick() {
    console.log("Button Clicked")
    if (onClick) onClick();
  }
</script>

<button on:click={handleClick} use:styleable={$component.styles} 
  class:is-selected={selected}    
  class:spectrum-ActionButton--emphasized={emphasized}
  class:spectrum-ActionButton--quiet={$buttonGroupStore?.quiet || quiet }
  class="spectrum-ActionButton spectrum-ActionButton--size{$buttonGroupStore?.size || size}"
  {disabled} >
  {#if icon && text != "" && !$buttonGroupStore?.iconOnly}
    <i style:padding-right={"0.5rem"} class="{icon}"/>
    <span class="spectrum-ActionButton-label">{text}</span>
  {:else if icon && $buttonGroupStore?.iconOnly }
    <i class="{icon} {size}"/>
  {:else}
   <span class="spectrum-ActionButton-label">{text}</span>
  {/if}
</button>
