<script setup lang="ts">
import { ref, useTemplateRef } from 'vue';

type UiTabsProps = {
    direction: 'horizontal' | 'vertical';
    items: string[];
};
const props = defineProps<UiTabsProps>();
const tabsIndicatorRef = useTemplateRef('tabsIndicatorRef'); // indicator element reference
const selectedItemIndex = ref(0); // select first item by default

const dir = props.direction === 'horizontal';
const itemWidth = dir ? 120 : 30;
const itemHeight = dir ? 30 : 120;

// handle indicator shift
const handleShift = (index: number) => {
    selectedItemIndex.value = index;
    if (tabsIndicatorRef.value) {
        if (dir) {
            tabsIndicatorRef.value.style.transform = `translateX(${index * itemWidth}px)`;
        } else {
            tabsIndicatorRef.value.style.transform = `translateY(${index * itemHeight}px)`;
        }
    }
}
</script>

<template>
    <ul class="ui-tabs" 
        :style="{
            '--flex-direction': dir ? 'row' : 'column',
            '--item-width': `${itemWidth}px`, 
            '--item-height': `${itemHeight}px`, 
            '--writing-mode': dir ? 'horizontal-tb' : 'vertical-lr',
        }"
    >
        <div ref="tabsIndicatorRef" class="ui-tabs-indicator"></div>
        <li v-for="(item, index) in props.items" 
            :key="index" 
            class="ui-tabs-item"
            :class="{active: selectedItemIndex === index}"
            @click="handleShift(index)"
        >
            {{ item }}
        </li>
    </ul>
</template>

<style scoped lang="scss">
.ui-tabs {
    position: relative;
    display: flex;
    flex-direction: var(--flex-direction);
    align-items: center;
    border: none;
    border-radius: min(var(--item-width), var(--item-height));
    background-color: #f5f5f5;
    box-shadow: 0 0 4px rgba(0, 0, 0, 0.15);
    z-index: 1;
}
.ui-tabs-indicator {
    position: absolute;
    left: 0;
    margin: auto 0;
    width: var(--item-width);
    height: var(--item-height);
    border: none;
    border-radius: min(var(--item-width), var(--item-height));
    background-color: #fff;
    z-index: 2;
    transition: transform 0.3s ease-in-out;
}
.ui-tabs-item {
    list-style: none;
    width: var(--item-width);
    height: var(--item-height);
    background-color: transparent;
    writing-mode: var(--writing-mode);
    user-select: none;
    font-size: 1.6rem;
    color: #333;
    text-align: center;
    line-height: min(var(--item-width), var(--item-height));
    cursor: pointer;
    z-index: 3;
    transition: font-weight 0.3s ease-in-out;

    &.active {
        font-weight: bold;
    }
}
</style>