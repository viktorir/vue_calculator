<template>
    <div class="window">
        <slot></slot>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.window {
    width: 100%;
    margin-bottom: 25px;
    overflow: hidden;

    display: flex;
    align-items: center;
    justify-content: flex-end;
}
</style>