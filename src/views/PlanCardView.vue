<template>
    <v-container fluid>
        <v-sheet class="sheet-border">
            <!-- <v-row class="ma-0 pa-0">
                <v-col class="ma-0 pa-0">
                    <span class="purple--text font-weight-black text-h3">Plans</span>
                    
                    <v-btn
                        class="mb-3 px-2 purple rounded-0 text-capitalize text-body-1"
                        dark
                        @click="toggleNewPlan = !toggleNewPlan"
                        depressed>
                        New Plan
                    </v-btn>
                </v-col>
            </v-row> -->
            <v-row
                class="ma-5 purple--text font-weight-black text-h3">
                <v-col md="6" offset="3" class="text-center">
                    <span>Plans</span>
                </v-col>
                <v-spacer></v-spacer>
                <v-col cols="2" class="text-right">
                    <v-btn
                        class="mb-3 px-2 purple rounded-0 text-capitalize text-body-1"
                        dark
                        @click="toggleNewPlan = !toggleNewPlan"
                        depressed>
                        New Plan
                    </v-btn>
                </v-col>
            </v-row>
            <v-row class="mb-5 mx-4 justify-space-between">
                <v-col
                    v-for="(plan, index) in plans" :key="plan.id"
                    md="6"
                    sm=12>
                    <PlanCardShow :plan="plan" @open-dialog="openEditDialog(index, plan)" />
                    <PlanEditDialog :plan="editPlan" :editId="editId" @close-dialog="closeDialog(index)" :dialog="open_dialog[index]" />
                </v-col>
            </v-row>
        </v-sheet>
    </v-container>
</template>
<script>
import PlanCardShow from '@/components/PlanCardShow'
import PlanEditDialog from '@/components/dialogs/PlanEditDialog'

export default {
    name: 'PlanCardView',
    components: {
        PlanCardShow,
        PlanEditDialog,
    },
    data() {
        return {
            toggleNewPlan: false,
            open_dialog: {},
            editId: -1,
            editPlan: {
                name: '',
                description: '',
            },
            plans: [
                {
                    id: 1,
                    name: 'Plan 1',
                    description: 'Plan 1 Description',
                    phases: [
                        {
                            name: 'Plan 1 Phase 1 Name',
                            description: 'Plan 1 Phase 1 Desc'
                        },
                        {
                            name: 'Plan 1 Phase 2 Name',
                            description: 'Plan 1 Phase 2 Desc'
                        }
                    ],
                },
                {
                    id: 2,
                    name: 'Plan 2',
                    description: 'Plan 2 Description',
                    phases: [
                        {
                            name: 'Plan 2 Phase 1 Name',
                            description: 'Plan 2 Phase 1 Desc'
                        },
                        {
                            name: 'Plan 2 Phase 2 Name',
                            description: 'Plan 2 Phase 2 Desc'
                        }
                    ],
                }
            ]
        }
    },
    methods: {
        openEditDialog(index, editPlan) {
            console.log('planId: ', planId)
            console.log('Before PlanCardView OpenDialog', this.open_dialog[index], index)
            // this.$set(this.open_dialog, index, this.open_dialog[index] = !this.open_dialog[index])
            this.$set(this.open_dialog, index, true)
            // this.open_dialog = !this.open_dialog
            console.log('After PlanCardView OpenDialog', this.open_dialog[index], index)
            // return this.open_dialog[index]
            this.editPlan.name = editPlan.name
            this.editPlan.description = editPlan.description


        },
        closeDialog(index) {
            this.$set(this.open_dialog, index, false)
        }
    }
}
</script>
<style lang="scss">
@import '@/scss/variables.scss';

.sheet-border {
    border: 1px solid $my-primary !important;
}
</style>