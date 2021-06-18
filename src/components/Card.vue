<template>
  <li>
    <a 
        :href="element.url"
        target="_blank"
        >
        <img 
            v-if="element.img"
            :src="element.img" 
            :alt="element.name">
        <h4>{{ element.name }}</h4>
    </a>
  </li>
</template>

<script>
export default {
    name: "Card",
    props: {
        element: {
            type: Object,
            required: true
        }
        // name: {
        //     type: String,
        //     required: true
        // },
        // url: {
        //     type: String,
        //     required: true
        // }
    }
}
</script>

<style lang="scss" scoped>
    @import '../styles/variables';

    li {
        list-style: none;
        width: calc(25% - 10px);
        margin: 5px;
        padding: 20px;
        text-align: center;
        background: $main-color;

        a {
            text-decoration: none;
            color: darken($main-color, 40%);
        }

        img {
            width: 60%;
        }
    }

</style>