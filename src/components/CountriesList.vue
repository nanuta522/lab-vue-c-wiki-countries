<template>
    <div class="container">
        <div class="row">
            <div class="col-md-5 list">
                <ul v-if="data" v-for="country in data" :key="country._id">
                    <router-link :to="`/list/${country.alpha3Code}`" style="text-decoration: none; color: inherit;">
                        <li @borderSelected="borderHandler" @click="countryHandler(country)">
                            <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`"
                                alt='flag image' /><br>
                            {{ country.name.official }}
                        </li>
                    </router-link>
                </ul>
            </div>

            <div class="col-md-1"></div>

            <div class="col-md-6 details sticky">
                <CountryDetails v-if="selectedCountry && data" :country="selectedCountry" :countryList="data"/>
            </div>
        </div>
    </div>
</template>

<script>
import CountryDetails from './CountryDetails.vue'

export default {
    components: {
        CountryDetails
    },
    data() {
        return {
            selectedCountry: null
        }
    },
    created() {
        let alpha3Code = this.$route.params.alpha3Code
        if (alpha3Code) this.selectedCountry = this.data.find(country => country.alpha3Code === alpha3Code)
    },
    props: {
        data: {
            type: Array,
            default: {}
        }
    },
    methods: {
        countryHandler(countryData) {
            this.selectedCountry = countryData
        },
        borderHandler(border) {
            this.borderName = border
        }
    },
    watch: {
        '$route.params.alpha3Code'() {
            if (this.data) this.selectedCountry = this.data.find(country => country.alpha3Code === this.$route.params.alpha3Code)
        }
    }
}
</script>

<style scoped>
.list {
    text-align: center;
}

li {
    border: 0.001rem outset rgb(218, 218, 218);
    padding: 2rem;
    margin-bottom: -1rem;
}

.sticky {
    position: fixed;
    right: 1rem;
}
</style>