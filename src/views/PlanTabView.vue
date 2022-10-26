<template>
    <v-container fluid>
        <v-row>
            <v-col
                md="12"
                sm=12>
                <v-sheet
                    class="pa-5"
                    outlined>
                    <v-tabs
                        v-model="tab"
                        dark
                        background-color="deep-purple accent-4">
                        <v-tab
                            v-for="plan in plans"
                            :key="plan.name">
                            {{ plan.name }}
                        </v-tab>
                    </v-tabs>

                    <v-tabs-items v-model="tab">
                        <v-tab-item
                            v-for="(plan, index) in plans"
                            :key="plan.id">
                            <v-row class="pa-0 ma-0 justify-space-around">
                                <v-btn
                                    @click="$set(togglePlanEdit, index, true)"
                                    class="rounded-0 mt-3 text-capitalize px-2"
                                    dark
                                    depressed>
                                    Create New Plan
                                    <v-icon right>mdi-plus</v-icon>
                                </v-btn>
                                <v-btn
                                    @click="$set(togglePlanDetails, index, !togglePlanDetails[index])"
                                    class="rounded-0 mt-3 text-capitalize px-2"
                                    dark
                                    depressed>
                                    {{ togglePlanDetails[index] ? "Hide Plan" : "View Plan" }}
                                    <v-icon right v-if="togglePlanDetails[index]">mdi-eye-off</v-icon>
                                    <v-icon right v-else>mdi-eye</v-icon>
                                </v-btn>
                                <v-btn
                                    v-if="togglePlanDetails[index]"
                                    @click="$set(togglePlanEdit, index, !togglePlanEdit[index])"
                                    class="rounded-0 mt-3 text-capitalize px-2"
                                    dark
                                    depressed>
                                    Edit Plan
                                    <v-icon right>mdi-pencil</v-icon>
                                </v-btn>
                            </v-row>

                            <PlanCardShow v-if="togglePlanDetails[index]" :plan="plan" :index="index" />
                            <PlanEditDialog
                                :dialog="togglePlanEdit[index]"
                                :plan="plan"
                                @close-dialog="$set(togglePlanEdit, index, !togglePlanEdit[index])" />

                            <v-sheet
                                v-for="phase in plan.phases"
                                :key="phase.name"
                                class="my-4"
                                color="deep-purple accent-4"
                                outlined>
                                <v-card
                                    outlined
                                    tile>
                                    <v-card-title>{{ phase.name }}</v-card-title>
                                    <v-card-text>{{ phase.description }}</v-card-text>
                                </v-card>
                            </v-sheet>
                        </v-tab-item>
                    </v-tabs-items>
                </v-sheet>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
import PlanCardShow from '@/components/PlanCardShow'
import PlanEditDialog from '@/components/dialogs/PlanEditDialog'

export default {
    name: 'PlanTabView',
    components: {
        PlanCardShow,
        PlanEditDialog,
    },
    data() {
        return {
            tab: null,
            togglePlanDetails: {},
            togglePlanEdit: {},
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
    }
}
</script>
<style lang="">
    
</style>