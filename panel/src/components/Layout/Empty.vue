<template>
  <component
    :is="element"
    :data-layout="layout"
    :type="element === 'button' ? 'button' : false"
    class="k-empty"
    v-on="$listeners"
  >
    <k-icon
      v-if="icon"
      :type="icon"
    />
    <p><slot /></p>
  </component>
</template>

<script>
export default {
  props: {
    text: String,
    icon: String,
    /**
     * Available options: `list`|`cards`
     */
    layout: {
      type: String,
      default: "list"
    }
  },
  computed: {
    element() {
      return this.$listeners["click"] !== undefined ? "button" : "div";
    }
  }
};
</script>

<style lang="scss">
/* global styles */
.k-empty {
  display: flex;
  align-items: stretch;
  border-radius: $rounded-xs;
  color: $color-gray-600;
  border: 1px dashed $color-border;
}
button.k-empty {
  width: 100%;
}
button.k-empty:focus {
  outline: none;
}
.k-empty p {
  font-size: $text-sm;
  color: $color-gray-600;
}
.k-empty > .k-icon {
  color: $color-gray-500;
}

/* layout:cards */
.k-empty[data-layout="cards"] {
  text-align: center;
  padding: 1.5rem;
  justify-content: center;
  flex-direction: column;

  .k-icon {
    margin-bottom: 1rem;
  }

  .k-icon svg {
    width: 2rem;
    height: 2rem;
  }
}

/* layout:list */
.k-empty[data-layout="list"] {
  min-height: 38px;

  & > .k-icon {
    width: 36px;
    min-height: 36px;
    border-right: 1px solid rgba($color-black, 0.05);
  }

  & > p {
    line-height: 1.25rem;
    padding: 0.5rem 0.75rem;
  }
}
</style>
