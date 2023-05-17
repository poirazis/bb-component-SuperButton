<script>
  import { getContext } from "svelte"


  export let size
  export let icon
  export let text
  export let emphasized
  export let quiet
  export let selected
  export let disabled

  const { styleable } = getContext("sdk")
  const component = getContext("component")

</script>

<button use:styleable={$component.styles} 
  class:is-selected={selected}    
  class:spectrum-ActionButton--emphasized={emphasized}
  class:spectrum-ActionButton--quiet={quiet}
  class="spectrum-ActionButton spectrum-ActionButton--size{size}"
  {disabled} >
  {#if icon && text != "" }
    <i style:padding-right={"0.5rem"} class="{icon} {size}"/>
    <span class="spectrum-ActionButton-label">{text}</span>
  {:else if icon }
    <i class="{icon} {size}"/>
  {:else}
   <span class="spectrum-ActionButton-label">{text}</span>
  {/if}
</button>
