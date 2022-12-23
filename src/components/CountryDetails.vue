<template>
    <div v-if="country" class="col-7" style="text-align: center;">
        <img v-if="country" :src="`https://flagpedia.net/data/flags/w580/${country.alpha2Code.toLowerCase()}.webp`"
            alt='flag image' width="300" /><br>
        <h1>{{ country.name.official }}</h1>
        <table class="table">
            <thead></thead>
            <tbody>
                <tr>
                    <td style="width: 50%;">Capital</td>
                    <td style="text-align: center;">{{ country.capital[0] }}</td>
                </tr>
                <tr>
                    <td>Area</td>
                    <td>
                        <sup>{{ country.area }}</sup>
                    </td>
                </tr>
                <tr>
                    <td>Borders</td>
                    <td style="text-align: center;">
                        <ul v-if="borders.length > 0" v-for="border in country.borders" :key="border">
                            <router-link :to="`/list/${border}`" style="text-decoration: none; color: inherit;"><li @click="borderHandler">{{ border }}</li></router-link>
                        </ul>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    data() {
        return {
            borders: this.country.borders,
            border: ''
        }
    },
    props: {
        country: {
            type: Object,
            default: {}
        },
        borderName: {
            type: String,
            default: ''
        }
    },
    methods: {
        borderHandler() {
            this.$emit('borderSelected', this.border)
        }
    }
}
</script>

<style>
.table {
    text-align: center;
}

img {
    margin-bottom: 2rem;
}
</style>