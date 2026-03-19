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
        id: "details",
        title: "Details",
        icon: "icons/dashboard.svg",
		darkmodeIcon: "icons/dashboard-darkmode.svg",
    },
    {
        id: "assortment",
        title: "Assortment",
    },
    {
        id: "questionnaires",
        title: "Questionnaires",
        icon: "icons/calendar-star.svg",
		darkmodeIcon: "icons/calendar-star-darkmode.svg",
        suffix: 32,
    },
    {
        id: "certificates",
        title: "Certificates",
		suffix: certificatesNum.value,
    },
    {
        id: "agreements",
        title: "Agreements",
        disabled: true,
		suffix: agreementsNum.value,
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

		<template #questionnaires>
			<h1>Questionnaires</h1>
			<p>
				This tab contains questionnaires.
			</p>
		</template>

		<template #certificates>
			<h1>Certificates</h1>
			<p>
				This tab shows certificate data.
			</p>
		</template>

		<template #agreements>
			<h1>Agreements</h1>
			<p>
				This tab contains agreement information once the tab is enabled.
			</p>
		</template>
	</TabbedContent>
</template>

<style lang="scss">
@use 'config' as *;

body {
	padding: 0;
	margin: 16px;
	background: var(--color-page-background);
	color: var(--color-surface-text-color);
}

</style>
