<template>
    <v-sheet outlined class="purple">
        <v-card flat outlined class="mt-0 rounded-0">
            <v-row class=" ma-0 pa-0">
                <v-col cols="12">
                    <v-img
                        class="text-center align-center white--text font-weight-black text-h4"
                        height="250"
                        src="@/assets/entrepreneur.jpg">
                        {{ plan.name }}
                    </v-img>
                </v-col>
            </v-row>
            <v-card-text class="pb-0">
                <v-textarea
                    v-model="plan.description"
                    readonly
                    label="Plan Description"
                    dense
                    class="rounded-0"
                    hide-details
                    outlined>
                </v-textarea>
            </v-card-text>
            <v-card-actions class="justify-center">
                <v-btn
                    class="purple rounded-0 mb-3 text-capitalize text-body-1 px-2"
                    dark
                    @click="openDialog(plan.id)"
                    depressed>
                    Edit Plan
                </v-btn>
                <!-- <PlanEditDialog
                    :dialog="toggleEditPlan"
                    :plan="plan"
                    @close-dialog="toggleEditPlan = !toggleEditPlan" /> -->
            </v-card-actions>
            <v-divider class="ma-4"></v-divider>
            <v-card-actions class="justify-center">
                <v-btn
                    class="green rounded-0 mb-0 text-capitalize text-body-1 px-2"
                    dark
                    depressed>
                    View Plan Details
                </v-btn>
            </v-card-actions>
            <v-card-actions class="justify-center pb-2">
                <v-chip
                    class="green darken-3 mr-1"
                    small
                    dark>
                    Phases: {{ plan.phases ? plan.phases.length : 0 }}
                </v-chip>
                <v-chip
                    class="green"
                    small
                    dark>
                    Stages: {{ plan.phases.stages ? plan.phases.stages.length : 0 }}
                </v-chip>
            </v-card-actions>
        </v-card>
    </v-sheet>
</template>
<script>
import PlanEditDialog from '@/components/dialogs/PlanEditDialog'

export default {
    name: 'PlanCardShow',
    props: {
        plan: Object
    },
    components: {
        PlanEditDialog,
    },
    data() {
        return {
            toggleEditPlan: false,
        }
    },
    methods: {
        openDialog(planId) {
            console.log('open edit dialog')
            this.$emit("open-dialog", planId);
        }
    }
}
</script>