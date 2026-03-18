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
		tabAllignment="left"
	>
		<template #details>
			<h1>Details</h1>
			<p>
				Here is the details page. you can see detailed information within this tab
			</p>
		</template>

		<template #assortment>
			<h1>Assortment</h1>
			<p>
				The entire assortment will be listed in this tab
			</p>
		</template>
	</TabbedContent>
</template>

<style lang="scss">

body {
	padding: 0;
	margin: 16px;
	background: #E5E5E5;
}

</style>