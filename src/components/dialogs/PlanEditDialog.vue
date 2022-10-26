<template>
    <v-dialog
        :value="dialog"
        @click:outside="closeDialog()"
        @input="$emit('input', $event)">
        <v-card flat outlined class="mt-2 rounded-0">
            <v-card-title>
                <v-text-field
                    v-model="plan.name"
                    label="Plan Name"
                    dense
                    class="rounded-0"
                    hide-details
                    outlined>
                </v-text-field>
            </v-card-title>
            <v-card-text>
                <v-textarea
                    v-model="plan.description"
                    label="Plan Description"
                    dense
                    class="rounded-0"
                    hide-details
                    outlined>
                </v-textarea>
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    class="rounded-0 mr-3"
                    dark
                    depressed
                    @click="closeDialog()">
                    Cancel
                </v-btn>
                <v-btn
                    class="rounded-0 mr-3"
                    dark
                    depressed>
                    Save
                </v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>
<script>
export default {
    name: 'PlanEditDialog',
    props: {
        plan: Object,
        dialog: Boolean,
    },
    data() {
        return {

        }
    },
    methods: {
        closeDialog() {
            this.$emit("close-dialog");
        },
        clickOutside() {
            console.log('clicked outside')
        }
    }
}
</script>