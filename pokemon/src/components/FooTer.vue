<template>
    <v-container>
        <v-row>
            <v-col cols="12">
                <v-footer class="d-flex flex-column">
                    <div class="bg-teal d-flex w-100 align-center px-4">
                    <strong>Contacta con nuestras redes sociales!</strong>

                    <v-spacer></v-spacer>

                    <v-btn
                        v-for="icon in icons"
                        :key="icon"
                        class="mx-4"
                        :icon="icon"
                        variant="plain"
                        size="small"
                    ></v-btn>
                    </div>

                    <div class="px-4 py-2 bg-black text-center w-100">
                    {{ new Date().getFullYear() }} — <strong>Adrián Santana Suárez</strong>
                    </div>
                </v-footer>
            </v-col>
        </v-row>
    </v-container>

</template>

<script>

export default {
    name: 'FooTer',

    data: () => ({

  }),
}
</script>

<style>

</style>
