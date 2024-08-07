<script>
  import { getContext } from "svelte";

  const { styleable } = getContext("sdk");
  const component = getContext("component");
  const buttonGroupStore = getContext("super-action-button-group");

  export let size;
  export let menuItem = false;
  export let menuAlign = "right";
  export let icon;
  export let fillOnHover;
  export let iconOnly;
  export let iconColor;
  export let hoverIcon;
  export let hoverIconColor;
  export let disabledIcon;
  export let text;
  export let textColor = "var(--spectrum-global-color-gray-700)";
  export let emphasized;
  export let quiet;
  export let selected;
  export let disabled;
  export let onClick;
  export let context;

  export let actionsMode;
  export let condition;
  export let onTrueCondition;
  export let onFalseCondition;
  export let loopSource;
  export let loopDelay;
  export let loopEvent;
  export let onLoopStart;
  export let onLoopEnd;

  $: useIcon = icon;
  $: useColor = iconColor;

  let working;

  async function handleClick() {
    if (actionsMode == "loop") {
      if (onLoopStart) await onLoopStart({ iterations: loopSource?.length });
      if (Array.isArray(loopSource) && loopEvent) {
        for (var i = 0; i < loopSource.length; i++) {
          await loopEvent({ idx: i, value: loopSource[i] });
          await sleep(loopDelay);
        }
      }
      if (onLoopEnd) await onLoopEnd();
    } else if (actionsMode == "conditional") {
      if (condition == true) await onTrueCondition?.();
      else await onFalseCondition?.();
    } else if (onClick) {
      await onClick({ context });
    }

    working = false;
    useIcon = hoverIcon
      ? hoverIcon
      : fillOnHover
        ? icon.replace("line", "fill")
        : icon;
  }

  function sleep(ms) {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }
</script>

<div class="super-component" use:styleable={$component.styles}>
  <button
    on:click={() => {
      working = true;
      useIcon = disabledIcon ? disabledIcon : icon;
      handleClick();
    }}
    on:mouseleave={!disabled && (hoverIcon || fillOnHover || hoverIconColor)
      ? () => {
          useIcon = icon;
          useColor = iconColor;
        }
      : () => {}}
    on:mouseenter={!disabled && (hoverIcon || fillOnHover || hoverIconColor)
      ? () => {
          useIcon = hoverIcon
            ? hoverIcon
            : fillOnHover
              ? icon?.replace("line", "fill")
              : icon;
          useColor = hoverIconColor || iconColor;
        }
      : () => {}}
    class:is-selected={selected}
    class:spectrum-ActionButton--emphasized={emphasized}
    class:spectrum-ActionButton--quiet={$buttonGroupStore?.quiet || quiet}
    class:menu-item={menuItem}
    class:menu-item-right={menuAlign == "right"}
    class="spectrum-ActionButton spectrum-ActionButton--size{$buttonGroupStore?.size ||
      size}"
    style:--iconColor={disabled
      ? "var(--spectrum-global-color-gray-400)"
      : useColor}
    disabled={disabled || working}
    style:background={$component.styles.normal["background-image"]}
  >
    {#if !iconOnly && icon && !$buttonGroupStore?.iconOnly}
      <i
        style:padding-right={text != "" ? "0.5rem" : "0rem"}
        class={disabled && disabledIcon ? disabledIcon : useIcon}
      />
      <span class="spectrum-ActionButton-label" style:color={textColor}
        >{text}</span
      >
    {:else if ($buttonGroupStore?.iconOnly || iconOnly) && icon}
      <i class={disabled && disabledIcon ? disabledIcon : useIcon} />
    {:else}
      <span class="spectrum-ActionButton-label" style:color={textColor}
        >{text}</span
      >
    {/if}
  </button>
</div>

<style>
  .menu-item {
    width: 100%;
    justify-content: flex-start;
  }
  .menu-item-right {
    width: 100%;
    justify-content: flex-end !important;
  }
  i {
    color: var(--iconColor);
    transition: all 230ms ease-in-out;
  }
</style>
