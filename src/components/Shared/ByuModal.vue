<template>
    <v-dialog width="400px" v-model="modal">
        <v-btn class="primary" flat slot="activator">Buy</v-btn>
        <v-card>
            <v-container>
                <v-layout row>
                    <v-flex xs12>
                        <v-card-title>
                            <h1 class="text--primary">Do you wan't to buy it ?</h1>
                        </v-card-title>
                    </v-flex>
                </v-layout>
                <v-divider></v-divider>
                <v-layout row>
                    <v-flex xs12>
                        <v-card-text>
                            <v-text-field
                                    name="name"
                                    label="You name"
                                    type="text"
                                    v-model="name"
                            ></v-text-field>
                            <v-text-field
                                    name="phone"
                                    label="You phone"
                                    type="text"
                                    multi-line
                                    v-model="phone"
                            ></v-text-field>
                        </v-card-text>
                    </v-flex>
                </v-layout>
                <v-divider></v-divider>
                <v-layout row>
                    <v-flex xs12>
                        <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn class="error"
                                   @click="onCancel"
                                   :dasabled="localLoading"
                            >Close
                            </v-btn>
                            <v-btn class="success"
                                   @click="onSave"
                                   :dasabled="localLoading"
                                   :loading="localLoading"
                            >Buy It</v-btn>
                        </v-card-actions>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-card>
    </v-dialog>
</template>

<script>
    /*eslint-disable */
    export default {
        props:['ad'],
        name: "ByuModal",
        data() {
            return {
                modal: false,
                name: '',
                phone: '',
                localLoading: false
            }
        },
        methods:{
            onCancel(){
                this.name = ''
                this.phone = ''
                this.modal = false
            },
            onSave(){
                if(this.name !== '' && this.phone !== ''){
                    this.localLoading = true
                    this.$store.dispatch('createOrder',{
                        name: this.name,
                        phone: this.phone,
                        adId: this.ad.id,
                        ownerId: this.ad.ownerId
                    })
                        .finally(() => {
                            this.name = ''
                            this.phone = ''
                            this.localLoading = false
                            this.modal = false
                        })
                }
            }
        }
    }
</script>

<style scoped>

</style>
