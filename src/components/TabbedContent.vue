<script setup>
import { computed, ref, defineProps } from 'vue';

const props = defineProps({
  tabs: {
    type: Array,
    required: true,
  },
  tabAllignment: { // 'left' or 'right'
    type: String,
    required: false,
  }
})

const tabSelectionIndex = ref(0);
const activeTabSlot = computed(() =>
    props.tabs?.[tabSelectionIndex.value]?.title?.toLowerCase()
);

// Function to select a tab unless its disabled
const selectTabByIndex = (tab, i) => {
    if (!tab.disabled)
        tabSelectionIndex.value = i;
}

</script>

<template>
    <div
        id="tabs"
        :style="`justify-content: ${
            props?.tabAllignment == 'right' ? 'flex-end' : 'flex-start'
        };`"
    >
        <div
            class="tab"
            :class="{ active: tabSelectionIndex === i, disabled: tab?.disabled ?? false }"
            v-for="tab, i in props.tabs"
            :key="i"
            @click="selectTabByIndex(tab, i)"
        >
            <!-- Tab icon -->
            <img :src="tab.icon" v-if="tab.icon" />

            <!-- Title -->
            {{ tab.title }}

            <!-- Suffix -->
            <span id="suffix">
                {{ tab.suffix }}
            </span>
        </div>
    </div>

    <div id="content">
        <slot :name="activeTabSlot" />
    </div>
</template>

<style scoped lang="scss">
@use '../config' as *;

#content {
    padding: 16px 8px;
    border-radius: 8px;
    background: var(--color-surface);
    border: 1px solid var(--color-border);
    color: var(--color-surface-text-color);
}

#tabs {
    margin-bottom: 10px;
    display: flex;
    gap: 5px;

    .tab {
        display: inline-flex;
        gap: 10px;
        padding: 16px 20px;
        color: var(--color-surface-text-color);
        border-radius: 8px;
        background: var(--color-surface);
        border: 1px solid var(--color-border);
        user-select: none;

        &:not(.disabled):hover {
            cursor: pointer;
            background: var(--color-tab-default-hover-background);
            border: 1px solid var(--color-tab-default-hover-border);
        }

        &.active {
            background: var(--color-tab-active);
            border: 1px solid var(--color-tab-active);

            &:hover {
                cursor: pointer;
                background: var(--color-tab-active-hover-background);
                border: 1px solid var(--color-tab-active-hover-border);
            }
        }

        &.disabled {
            color: var(--color-muted-text);
            background: var(--color-tab-disabled-background);
        }

        #suffix {
            color: var(--color-muted-text);
        }
    }
}

</style>
