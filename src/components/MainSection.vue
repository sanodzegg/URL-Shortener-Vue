<script>
    export default {
        data() {
            return {
                i: localStorage.length,
                error: false,
                inputText: '',
                errText: 'Please add a link',

                shortened: 'test',
                original: 'test2',

                shortList: [],
                localList: []
            }
        },
        computed : {
            handleInput(){
                return {
                    'error' : this.error,
                }
            }
        },
        mounted:function() {
            Object.values(localStorage).forEach(e => {
                this.localList.push(JSON.parse(e));
            });
        },
        methods: {
            handleClick() {
                if(this.inputText.length > 0) {
                    this.error = false;
                    fetch(`https://api.shrtco.de/v2/shorten?url=${this.inputText}`).then(res => res.json())
                    .then(data => {

                        let dataToPush =  {
                            original:data.result.original_link,
                            shortened:data.result.full_short_link
                        };

                        if(data.ok == true) {
                            this.error = false;
                            this.shortList.push(dataToPush);
                            localStorage.setItem(this.i, [JSON.stringify(...this.shortList)]);
                            this.i++;

                            this.localList.push(dataToPush);
                        } else {
                            this.errText = `${data.error}`;
                            this.error = true;
                        }
                    });
                } else {
                    this.error = true;
                }
            },
            copy(item, event) {
                let btn = event.target;
                try {
                    navigator.clipboard.writeText(item.shortened);

                    btn.classList.add("copied");
                    btn.innerText = "Copied";
                } catch(err) {
                    throw err;
                }
                
            }
        }
    }
</script>

<template>
    <section class="main">
        <div class="main__landing">
            <div class="main__text">
                <h1></h1>
                <h5>Build your brand's recognition and get 
                    detailed insights on how your links are performing.</h5>
                <a href="#"><button>Get Started</button></a>
            </div>
            <div class="main__img">
                <img src="../../public/images/illustration-working.svg" alt="illustration">
            </div>
        </div>
        <div class="main__input">
            <div class="input__wrapper">
                <div class="input">
                    <input type="text" placeholder="Shorten a link here..." v-model="inputText" :class="handleInput">
                    <p v-bind:class="handleInput">{{ errText }}</p>
                </div>
                <button v-on:click="handleClick">Shorten it!</button>
            </div>
        </div>

        <div class="shortened__list">
            <div class="shortened__wrapper" v-for="item in localList" :key="item">
                <p class="shortened__original">{{ item.original }}</p>
                <div class="shortened__l">
                    <p class="shortened__active">{{ item.shortened }}</p>
                    <button class="shortened__copy" v-on:click="copy(item, $event)">Copy</button>
                </div>
            </div>
        </div>
    </section>
</template>