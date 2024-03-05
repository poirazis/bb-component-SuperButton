
<script>
  import { getContext } from "svelte"

  const { styleable } = getContext("sdk")
  const component = getContext("component")
  const buttonGroupStore = getContext("super-action-button-group")

  export let size
  export let icon
  export let iconOnly
  export let text
  export let emphasized
  export let quiet
  export let selected
  export let disabled
  export let onClick

  export let loopActions
  export let loopSource
  export let loopDelay
  export let loopEvent
  export let onLoopStart
  export let onLoopEnd

  async function handleClick() {
    if ( loopActions ) {
      disabled = true;
      if ( onLoopStart ) onLoopStart( { iterations : loopSource?.length } )
      if ( Array.isArray(loopSource) && loopEvent ) {
        for (var i = 0; i < loopSource.length; i++) {
          loopEvent({idx : i, value: loopSource[i]})
          await sleep(loopDelay);
         }
      }
      if ( onLoopEnd ) onLoopEnd();
      disabled = false;
    } else if (onClick) {
      disabled = true;
      onClick();
      disabled = false;
    }
  }

  function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }
</script>

<div use:styleable={$component.styles} >
  <button 
    on:click={handleClick} use:styleable={$component.styles} 
    class:is-selected={selected}    
    class:spectrum-ActionButton--emphasized={emphasized}
    class:spectrum-ActionButton--quiet={$buttonGroupStore?.quiet || quiet }
    class="spectrum-ActionButton spectrum-ActionButton--size{$buttonGroupStore?.size || size}"
    {disabled} >
    {#if icon && !$buttonGroupStore?.iconOnly && !iconOnly}
      <i style:padding-right={ text != "" ? "0.5rem" : "0rem"} class="{icon}"/>
      <span class="spectrum-ActionButton-label">{text}</span>
    {:else if icon && ($buttonGroupStore?.iconOnly || iconOnly )}
      <i class="{icon} {size}"/>
    {:else}
    <span class="spectrum-ActionButton-label">{text}</span>
    {/if}
  </button>
</div>

<style>
  .spectrum-ActionButton--emphasized:hover {
    color: var(--primaryColor);
  }
</style>














