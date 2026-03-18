<script setup>
import { ref } from 'vue';

const tabs = ref([
    {
        title: "Details",
        icon: "icons/dashboard.svg"
    },
    {
        title: "Assortment",
    },
    {
        title: "Questionnaires",
        icon: "icons/calendar-star.svg",
        suffix: 32,
    },
    {
        title: "Certificates",
    },
    {
        title: "Agreements",
    },
]);

const tabSelectionIndex = ref(0);
const tabAllignment = ref("left"); // 'right' or 'left'

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
            :class="{ active: tabSelectionIndex === i }"
            v-for="tab, i in tabs"
            :key="i"
            @click="tabSelectionIndex = i"
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

        &.active {
            background: #D3A9FF;
            border: none;
        }

        &:hover {
            cursor: pointer;
        }

        #suffix {
            color: #666;
        }
    }
}

</style>