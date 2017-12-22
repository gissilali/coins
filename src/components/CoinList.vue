<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8 offset-2">
                <b-table :items="items"
                         :fields="fields">
                </b-table>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "coin-list",
        mounted: function () {
            this.getAllCurrencies();
        },
        data() {
            return {
                fields: ['Id', '', 'Name', 'Algorithm', 'Sponsored'],
                items: []
            }
        },
        methods: {
            getAllCurrencies() {
                let url = 'https://min-api.cryptocompare.com/data/all/coinlist';
                let coins = [];
                var vm = this;
                let request = axios.get(url)
                    .then(response => {
                        coins = response.data.Data;
                        for(var propName in coins) {
                            if (coins.hasOwnProperty(propName)) {
                                this.items.push(coins[propName]);
                            }
                        }
                    });
            }
        }
    }
</script>

<style scoped>
    
</style>