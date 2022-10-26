<template>
    <v-card>
        <v-app-bar
            height="250"
            prominent
            gradient="rgba(0, 0, 0, 0)"
            src="@/assets/entrepreneur.jpg"
            flat>

            <template v-slot:img="{ props }">
                <v-img
                    v-bind="props"
                    gradient="to top right, rgba(19, 84, 122, .5), rgba(19, 84, 122, .8)">
                </v-img>
            </template>

            <v-app-bar-nav-icon color="white" @click="displayMenu = !displayMenu">
                <v-list-item v-if="displayMenu">
                    Bob
                </v-list-item>
            </v-app-bar-nav-icon>
            <v-spacer></v-spacer>
            <span class="ml-9 mt-2 text-h5 font-weight-black white--text">
                {{ plan.name }}
            </span>

        </v-app-bar>

        <v-card-text class="">
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
            <span class="green--text font-weight-bold">Plan Details:</span>
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
</template>
<script>
import PlanEditDialog from '@/components/dialogs/PlanEditDialog'

export default {
    name: 'PlanCardShow',
    props: {
        plan: Object,
        editId: Number,
    },
    components: {
        PlanEditDialog,
    },
    data() {
        return {
            toggleEditPlan: false,
            displayMenu: false,
        }
    },
    methods: {
        openDialog(planId) {
            console.log('open edit dialog')
            this.$emit("open-dialog");
        }
    }
}
</script>