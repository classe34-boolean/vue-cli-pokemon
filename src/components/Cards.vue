<template>
  <ul>
    <Card 
        v-for="item in items"
        :key="item.url"
        :element="item"
    />
  </ul>
</template>

<script>
import Card from './Card';

export default {
    name: "Cards",
    props: {
        items: {
            type: Array,
            required: true
        }
    },
    components: {
        Card
    }
}
</script>

<style lang="scss" scoped>
    ul {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
</style>