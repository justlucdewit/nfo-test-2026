<script setup>
import { computed, ref, defineProps, onMounted, onBeforeUnmount } from 'vue';

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
    props.tabs?.[tabSelectionIndex.value]?.id
);
const prefersDarkMode = ref(false);

let darkModeMediaQuery;

const syncDarkModePreference = (event) => {
    prefersDarkMode.value = event.matches;
};

// On mount, set event listener to change of the prefers-color-scheme media query
// to sync the state to a boolean variable.
onMounted(() => {
    darkModeMediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
    prefersDarkMode.value = darkModeMediaQuery.matches;
    darkModeMediaQuery.addEventListener('change', syncDarkModePreference);
});

// on before unmount, remove the event listener.
onBeforeUnmount(() => {
    darkModeMediaQuery?.removeEventListener('change', syncDarkModePreference);
});

// Function to select a tab unless its disabled
const selectTabByIndex = (tab, i) => {
    if (!tab.disabled)
        tabSelectionIndex.value = i;
}

// Function to get the public URI to the icon needed for
// this tab, based on dark/lightmode preference
const getTabIcon = (tab) => {
    if (prefersDarkMode.value && tab.darkmodeIcon)
        return tab.darkmodeIcon;

    return tab.icon;
};

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
            <img :src="getTabIcon(tab)" v-if="getTabIcon(tab)" />

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
    overflow-x: auto;

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
