<script setup>
import { ref } from 'vue';

const tabs = ref([
    {
        title: "First tab",
    },
    {
        title: "Second tab",
    },
    {
        title: "Third tab",
    },
]);
</script>

<template>
    <div id="tabs">
        <div class="tab active" v-for="tab, i in tabs" :key="i">
            {{ tab.title }}
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
        display: inline-block;
        padding: 16px 8px;
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
    }
}

</style>