<template>
    <div v-if="suggestion">
        <slot/>
        <span class="mail-check" @click.stop="UpdateParent()">{{ suggestion }} ?</span>
    </div>
</template>

<style>
    .mail-check {
        cursor: pointer;
        color: red;
    }
</style>

<script>
import Mailcheck from 'mailcheck'

export default {
    props: {
        modelName: {
            type: String,
            required: true
        },
        data: {
            type: String,
            required: true
        },
        domains: {
            type: Array,
            required: false,
            default: () => {
                return Mailcheck.defaultDomains
            }
        },
        topLevelDomains: {
            type: Array,
            required: false,
            default: () => {
                return Mailcheck.topLevelDomains
            }
        },
        secondLevelDomains: {
            type: Array,
            required: false,
            default: () => {
                return Mailcheck.secondLevelDomains
            }
        },
        distanceFunction: {
            type: Function,
            required: false
        }
    },
    data() {
        return {
            suggestion: null
        }
    },
    methods: {
        verifyEmail() {
            let vm = this

            Mailcheck.run({
                email: vm.data,
                domains: this.domains,                       // optional
                topLevelDomains: this.topLevelDomains,       // optional
                secondLevelDomains: this.secondLevelDomains, // optional
                distanceFunction: this.distanceFunction,     // optional
                suggested: (suggestion) => {
                    vm.suggestion = suggestion.full
                },
                empty: () => {}
            })
        },
        UpdateParent() {
            this.$parent[this.modelName] = this.suggestion
            this.suggestion = null
        }
    },
    watch: {
        data: 'verifyEmail'
    }
}
</script>
