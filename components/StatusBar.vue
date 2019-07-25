<template>
    <view>
        <view class="header" :style="{backgroundColor: color}">
        </view>
    </view>
</template>

<script>
    export default {
        props: ['color']
    }
</script>

<style>
    .header {
        height: 34px;
    }
</style>
