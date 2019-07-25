<template>
    <Root>
    <view class="container">
        <!-- <app-loading v-if="!isAppReady"></app-loading> -->
        <LandingPage v-if="!isAppReady"></LandingPage>
        <app v-else></app>
    </view>
    </Root>
</template>

<script>
    import Vue from "vue-native-core";
    import { StackNavigator } from "vue-native-router";
    import {  Root, VueNativeBase } from "native-base";
    import { AppLoading } from "expo";
    import App from "./components/App";
    import LandingPage from "./components/LandingPage";

    // registering all native-base components to the global scope of the Vue
    Vue.use(VueNativeBase);
    export default {
        components: {
            App, AppLoading, Root, LandingPage
        },
        data: function() {
            return {
                isAppReady: false
            };
        },
        created: function() {
            this.loadFonts();
        },
        methods: {
            loadFonts: async function() {
                try {
                    this.isAppReady = false;
                    await Expo.Font.loadAsync({
                        Roboto: require("native-base/Fonts/Roboto.ttf"),
                        Roboto_medium: require("native-base/Fonts/Roboto_medium.ttf"),
                        // Ionicons: require("@expo/vector-icons/fonts/Ionicons.ttf")
                    });
                    setTimeout(()=> this.isAppReady = true, 2000);
                } catch (error) {
                    console.log("some error occured", error);
                    this.isAppReady = true;
                }
            }
        }
    };
</script>

<style>
    .container {
        flex: 1;
    }
</style>
