<template>
    <div class="col-7" style="text-align: center;">
        <img v-if="country" :src="`https://flagpedia.net/data/flags/w580/${country.alpha2Code.toLowerCase()}.webp`"
            alt='flag image' width="300" /><br>
        <h1>{{ country.name.official }}</h1>
        <table class="table">
            <thead></thead>
            <tbody>
                <tr>
                    <td style="width: 50%;">Capital</td>
                    <td v-if="country" style="text-align: center;">{{ country.capital[0] }}</td>
                </tr>
                <tr>
                    <td>Area</td>
                    <td>
                        <sup v-if="country">{{ country.area }}</sup>
                    </td>
                </tr>
                <tr>
                    <td>Borders</td>
                    <td style="text-align: center;">
                        <ul v-if="borders.length > 0" v-for="border in country.borders" :key="border">
                            <router-link :to="`/list/${border}`" style="text-decoration: none; color: inherit;">
                                <li @click="borderHandler">{{ countryList.length ? border = countryList.find(country =>
        country.alpha3Code ===
        border).name.common : border
}}</li>
                            </router-link>
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
        },
        countryList: {
            type: Array,
            default: []
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