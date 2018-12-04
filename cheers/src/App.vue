<template>
    <v-app dark color="primary">
        <v-toolbar app color="primary" dark>
            <v-toolbar-title class="headline text-uppercase">
                <span class="font-weight-light accent--text">CHEERS</span>
                <span class="accent--text">&nbsp;Counter</span>
            </v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn @click="reset">Reset</v-btn>
        </v-toolbar>
        <v-content>
            <v-container fluid fill-height>
                <v-layout align-center justify-center>
                    <v-flex d-flex xs6>
                        <v-card class="elevation-3" color="primary" @click="cheers">
                            <v-card-text>
                                <v-container fluid fill-height>
                                    <v-layout align-center justify-center>
                                        <v-flex d-flex xs12 text-xs-center ma-5>
                                            <span class="display-4 text-uppercase font-weight-light accent--text"
                                                  v-text="count">0</span>
                                        </v-flex>
                                    </v-layout>
                                </v-container>
                            </v-card-text>
                        </v-card>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
    import ss from 'sessionstorage'

    export default {
        name: 'Home',
        data: () => ({
            count: 0
        }),
        mounted() {
            if (ss.getItem('cheers') !== undefined) {
                this.count = ss.getItem('cheers')
            } else {
                this.zeroCount()
            }
        },
        methods: {
            zeroCount() {
                this.count = 0
                ss.setItem('cheers', 0)
            },
            cheers() {
                this.count++
                ss.setItem('cheers', this.count)
            },
            reset() {
                ss.clear()
                this.zeroCount()
            }
        }
    }
</script>
