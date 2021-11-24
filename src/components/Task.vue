<template>
    <v-container>
        <v-row class="d-flex justify-center">
            <v-col cols="12" sm="9" md="6">
                <v-card color="theme--dark" dark>
                    <v-container class="d-flex flex-column">
                        <v-text-field label="Titulo" v-model="$route.params.id.title"></v-text-field>
                        <v-textarea rows="1" label="Descripción" auto-grow v-model="$route.params.id.description"></v-textarea>
                    </v-container>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
export default {
    data: function() {
        return {
            item: {
                title: '$route.params.id.title',
                description: '$route.params.id.description', 
                isCompleted: '$route.params.id.isCompleted'
            }
        }
    }
}
</script>