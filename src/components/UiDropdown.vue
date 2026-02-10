<script setup lang="ts">
type UiDropdownProps = {
    label: string;
    options: string[];
}
const props = defineProps<UiDropdownProps>();
</script>

<template>
    <button class="ui-dropdown">
        <p class="label">{{ props.label }}</p>
        <ul class="options">
            <li v-for="(item, index) in props.options" 
                :key="index"
                class="item"
            >
                {{ item }}
            </li>
        </ul>
    </button>
</template>

<style scoped lang="scss">
.ui-dropdown {
    position: relative;
    min-width: 160px;
    height: 40px;
    border: none;
    border-radius: 20px;
    background-color: #fff;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.15);
    cursor: pointer;
    transition: background-color 0.3s ease;

    &:hover {
        background-color: #f5f5f5;
        .options {
            visibility: visible;
            opacity: 1;
        }
    }
}
.label {
    font-size: 1.6rem;
    color: var(--black);
    text-align: center;
}
.options {
    position: absolute;
    top: calc(100% + 10px);
    left: 50%;
    transform: translateX(-50%);
    background-color: #fff;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.15);
    visibility: hidden;
    opacity: 0;
    transition: all 0.3s ease;
}
.options .item {
    list-style: none;
    min-width: 250px;
    height: 40px;
    border-bottom: 1px solid #f5f5f5;
    background-color: #fff;
    font-size: 1.4rem;
    color: var(--gray);
    text-align: center;
    line-height: 40px;
    transition: background-color 0.3s ease;
    &:hover {
        background-color: #f5f5f5;
    }
}
</style>