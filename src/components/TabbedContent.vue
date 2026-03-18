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
@use '../styles/config' as *;

#content {
    padding: 16px 8px;
    border-radius: 8px;
    background: $color-surface;
    border: $color-border;
}

#tabs {
    margin-bottom: 10px;
    display: flex;
    gap: 5px;

    .tab {
        display: inline-flex;
        gap: 10px;
        padding: 16px 20px;
        border-radius: 8px;
        background: $color-surface;
        border: $color-border;
        user-select: none;

        &.active {
            background: $color-tab-active;
            border: none;
        }

        &.disabled {
            color: $color-muted-text;
            background: $color-tab-disabled-background;
        }

        &:not(.disabled):hover {
            cursor: pointer;
        }

        #suffix {
            color: $color-muted-text;
        }
    }
}

</style>
