# NFO Frontend Test

This project contains my solution for the NFO 2026 frontend test.

The goal was to build a reusable tab component in Vue based on the provided Figma design, including support for light and dark mode.

## Project structure

- [src/components/TabbedContent.vue](/home/lucdewit/projects/nfo-test-2026/src/components/TabbedContent.vue): main tab component
- [src/App.vue](/home/lucdewit/projects/nfo-test-2026/src/App.vue): simple example usage
- [src/config.scss](/home/lucdewit/projects/nfo-test-2026/src/config.scss): light and dark theme variables
- [src/thoughts.md](/home/lucdewit/projects/nfo-test-2026/src/thoughts.md): notes about things I would still improve

## Running the project

Install dependencies:

```bash
yarn
```

Start the dev server:

```bash
yarn dev
```

Build for production:

```bash
yarn build
```

Preview the production build:

```bash
yarn preview
```

## Component usage

The component accepts a `tabs` array.

Each tab can have:

- `id`: stable identifier used for the slot name
- `title`: label shown in the tab button
- `icon`: icon used in light mode, or as fallback in dark mode
- `darkmodeIcon`: optional icon used when dark mode is active
- `suffix`: optional extra content shown on the right side
- `disabled`: disables the tab

Example:

```jsx
const tabs = [
  {
    id: 'details',
    title: 'Details',
    icon: 'icons/dashboard.svg',
    darkmodeIcon: 'icons/dashboard-darkmode.svg',
  },
  {
    id: 'assortment',
    title: 'Assortment',
    suffix: 12,
  },
]


<TabbedContent
    :tabs="tabs"
    tabAllignment="left"
>
    <template #details>
      <div>Details content</div>
    </template>

    <template #assortment>
      <div>Assortment content</div>
    </template>
</TabbedContent>
```
