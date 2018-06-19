<template>
    <div>
        <div class="container">
            <h1>Mergesort - Divide et Impera</h1>
            <h3>Introduceti sirul de numere:</h3>
            <input type="text" class="form-control" id="exampleFormControlInput2" v-model="a"
                   placeholder="Introduceti sirul de numere:">
            <br>
            <button type="button" class="btn btn-secondary" v-on:click="sortare(a)">
                Ordoneaza sirul!
            </button>
            <br><br>

            <h3 v-if="sirOrdonat">Sirul ordonat este:</h3>
            {{ sirOrdonat }}

        </div>


    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                a: '',
                sirOrdonat: '',
            }
        },
        methods: {
            merge: function (sirStanga, sirDreapta) {
                var result = [];
                //cat timp exista elememte in cele doua siruri
                while (sirStanga.length && sirDreapta.length) {
                    if (sirStanga[0] <= sirDreapta[0]) {
                        result.push(sirStanga.shift());
                    } else {
                        result.push(sirDreapta.shift());
                    }
                }
                while (sirStanga.length) {
                    result.push(sirStanga.shift());
                }
                while (sirDreapta.length) {
                    result.push(sirDreapta.shift());
                }
                return result;
            },
            mergesortDiv: function (a) {
                if (a.length < 2) {
                    return a;
                } else {
                    var mijloc = a.length / 2;
                    var stanga = a.slice(0, mijloc);
                    var dreapta = a.slice(mijloc, a.length);
                }
                return this.merge(this.mergesortDiv(stanga), this.mergesortDiv(dreapta));
            },
            sortare: function (a) {
                a = a.split(',').map(function (item) {
                    return parseInt(item, 10);
                });
                this.sirOrdonat = this.mergesortDiv(a);

                console.log(this.sirOrdonat);
            }
        }
    }
</script>

<style lang="scss">

</style>