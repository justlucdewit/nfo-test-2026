<script setup>
import { onBeforeUnmount, onMounted, shallowRef } from 'vue'

import TabbedContent from './components/TabbedContent.vue'

let certificatesNum = shallowRef(10)
let agreementsNum = shallowRef(99)
let interval = shallowRef(null)

onMounted(() => {
	interval.value = setInterval(() => {
		certificatesNum.value = Math.floor(Math.random() * 100)
		agreementsNum.value = Math.floor(Math.random() * 100)
	}, 2000)
})

onBeforeUnmount(() => {
	clearInterval(interval.value)
})

const tabs = [
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
        disabled: true
    },
];

</script>

<template>
	<h1>Let's build some tabs!</h1>

	<TabbedContent
		:tabs="tabs"
	/>
</template>

<style lang="scss">

body {
	padding: 0;
	margin: 16px;
	background: #E5E5E5;
}

</style>