<template>
    <div v-if="suggestion">
        <slot/>
        <span class="mail-check" @click.stop="UpdateParent()">{{ suggestion }} ?</span>
    </div>
</template>

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
                return Mailcheck.defaultTopLevelDomains
            }
        },
        secondLevelDomains: {
            type: Array,
            required: false,
            default: () => {
                return Mailcheck.defaultSecondLevelDomains
            }
        },
        distanceFunction: {
            type: Function,
            required: false,
            default: Mailcheck.sift4Distance
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
                domains: vm.domains,                       // optional
                topLevelDomains: vm.topLevelDomains,       // optional
                secondLevelDomains: vm.secondLevelDomains, // optional
                distanceFunction: vm.distanceFunction,     // optional
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
