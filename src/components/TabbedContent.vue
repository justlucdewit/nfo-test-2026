<script setup>
import { ref, defineProps } from 'vue';

const props = defineProps({
  tabs: {
    type: Array,
    required: true,
  },
})

const tabSelectionIndex = ref(0);
const tabAllignment = ref("left"); // 'right' or 'left'

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
            tabAllignment == 'right' ? 'flex-end' : 'flex-start'
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
        <h1>Contents of the TabPannel</h1>
        <h2>Contents of the TabPannel</h2>
        <h3>Contents of the TabPannel</h3>
        <h4>Contents of the TabPannel</h4>
        <h5>Contents of the TabPannel</h5>
        <h6>Contents of the TabPannel</h6>
    </div>
</template>

<style scoped lang="scss">

#content {
    padding: 16px 8px;
    border-radius: 8px;
    background: white;
    border: #CCC;
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
        background: white;
        border: #CCC;
        user-select: none;

        &.active {
            background: #D3A9FF;
            border: none;
        }

        &.disabled {
            color: #666;
            background: #F2F2F2;
        }

        &:not(.disabled):hover {
            cursor: pointer;
        }

        #suffix {
            color: #666;
        }
    }
}

</style>