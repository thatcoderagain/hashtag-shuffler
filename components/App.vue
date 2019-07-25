<template>
    <nb-container  class="background">
        <StatusBar :color="'#34495e'"></StatusBar>
        <nb-content>
            <nb-h1 class="title">Hashtag Shuffler</nb-h1>
            <nb-card class="card">
                <nb-card-item header>
                    <nb-h3>Paste your hashtags here</nb-h3>
                </nb-card-item>
                <nb-card-item>
                    <nb-content>
                        <nb-form>
                            <nb-textarea v-model="textInput" class="textInput padding-10" :rowSpan="8" bordered placeholder="#love #nature #beautiful #picoftheday #follow4folow" />
                        </nb-form>
                    </nb-content>
                </nb-card-item>
                <nb-card-item class="flexCenter">
                    <nb-card class="flexCenter flexBox">
                        <nb-button danger class="button" :onPress="shuffle">
                            <nb-icon name="shuffle" />
                        </nb-button>
                        <nb-button info class="button" :onPress="() => {textInput='', hashtags=[]}">
                            <nb-text>Clear</nb-text>
                        </nb-button>
                        <nb-button warning class="button" :onPress="copy">
                            <nb-text>Copy All</nb-text>
                        </nb-button>
                        <nb-button success class="button" :onPress="copy30">
                            <nb-text>Copy 30 Hashtags</nb-text>
                        </nb-button>
                    </nb-card>
                </nb-card-item>
                <nb-card-item footer>
                    <nb-card v-if="hashtags.length > 0" class="padding-10 flexBox">
                        <nb-badge info v-for="hashtag in hashtags" class="margin-4 flexBox">
                            <nb-text class="badge"> {{ hashtag }} </nb-text>
                        </nb-badge>
                    </nb-card>
                </nb-card-item>
            </nb-card>
        </nb-content>
    </nb-container>
</template>

<script>
    import StatusBar from './StatusBar';
    import { Clipboard } from 'react-native';
    import { Toast } from "native-base";

    export default {
        components: {
            StatusBar
        },
        data() {
            return {
                textInput: '',
                hashtags: []
            }
        },
        methods: {
            shuffle() {
                if (this.textInput.trim().length == 0) {
                    this.toast("No hashtags found", "danger");
                    return;
                }
                this.hashtags = this.textInput.split(' ');
                this.hashtags = this.hashtags.filter((hashtag) => {
                    if (hashtag.trim().length != 0)
                        return hashtag;
                }).map((hashtag) => {
                    if (!hashtag.startsWith('#'))
                        return '#' + hashtag.trim();
                    else
                        return hashtag.trim();
                });
                this.hashtags = this.shuffler(this.hashtags);
            },
            shuffler(arr) {
                let ctr = arr.length, temp, index;
                while (ctr > 0) {
                    index = Math.floor(Math.random() * ctr);
                    ctr--;
                    temp = arr[ctr];
                    arr[ctr] = arr[index];
                    arr[index] = temp;
                }
                return arr;
            },
            async copy() {
                if (this.hashtags.length == 0) {
                    this.shuffle();
                }
                if (this.textInput == '' || this.hashtags.length == 0) {
                    this.toast("No Hashtags Found", "danger");
                    return ;
                }
                let str = this.hashtags.join(' ');
                await Clipboard.setString(str);
                this.toast("All shuffled hashtags are copied", "warning");
            },
            async copy30() {
                if (this.hashtags.length == 0) {
                    this.shuffle();
                }
                if (this.textInput == '' || this.hashtags.length == 0) {
                    this.toast("No Hashtags Found", "danger");
                    return ;
                }
                let str = this.hashtags.slice(0,30).join(' ');
                await Clipboard.setString(str);
                this.toast("First 30 shuffled hashtags are Copied", "success");
            },
            toast(string, type) {
                Toast.show({
                    text: string,
                    buttonText: "Okay",
                    duration: 2000,
                    type: type
                });
            }
        }
    }
</script>

<style scoped>
    .flexCenter {
        flex: 1;
        align-items: center;
        justify-content: center;
    }
    .flexBox {
        display: flex;
        flex-wrap: wrap;
        flex-direction: row;
    }
    .title {
        padding: 20px;
        text-align: center;
        background-color: #34495e;
        color: #ffffff;
        font-weight: 800;
    }
    .background {
        background-color: #41b883;
    }
    .textInput {
        font-size: 16px;
    }
    .button {
        margin-top: 5px;
        margin-bottom: 5px;
        margin-left: 5px;
        margin-right: 5px;
    }
    .card {
        margin-top: 10px;
        margin-bottom: 10px;
        margin-left: 10px;
        margin-right: 10px;
    }
    .badge {
        padding: 4px;
        font-size: 18px;
    }
    .margin-4 {
        margin-top: 4px;
        margin-bottom: 4px;
        margin-left: 4px;
        margin-right: 4px;
    }
    .padding-10 {
        padding-left: 10px;
        padding-bottom: 10px;
        padding-top: 10px;
        padding-right: 10px;
    }
</style>
