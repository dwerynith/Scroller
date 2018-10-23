<template>
    <div id="home" class=".home-body">
        <div class="back">
            <div class="buttons-container">
                <div class="header">
                    <h1>
                        Title
                    </h1>
                </div>
                <div class="buttons">
                    <div class="hline"/>
                    <div class="faded-back">
                        Quick Actions
                    </div>
                    <div class="hline"/>
                    <div
                        class="app"
                        @touchstart="touchStart"
                        @touchend="touchEnd"
                        @touchmove="touchMove"
                        @mousedown="touchStart"
                        @mouseup="touchEnd"
                        @mouseleave="touchMove">
                        <div style="grid-column: 2">
                            All OFF
                        </div>
                    </div>
                    <div class="hline"/>
                    <div class="faded-back">
                        Apps
                    </div>
                    <div class="hline"/>
                    <div
                        class="app"
                        @click="openTv"
                        @touchstart="touchStart"
                        @touchend="touchEnd"
                        @touchmove="touchMove"
                        @mousedown="touchStart"
                        @mouseup="touchEnd"
                        @mouseleave="touchMove">
                        <div style="grid-column: 2">
                            TV
                        </div>
                    </div>
                    <div class="hline"/>
                    <div
                        class="app"
                        @click="openMusic"
                        @touchstart="touchStart"
                        @touchend="touchEnd"
                        @touchmove="touchMove"
                        @mousedown="touchStart"
                        @mouseup="touchEnd"
                        @mouseleave="touchMove">
                        <div style="grid-column: 2">
                            Music
                        </div>
                    </div>
                    <div class="hline"/>
                    <div class="app"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Home",
        methods: {
            openTv() {},
            openMusic() {},
            touchStart(event) {
                if (event.target.classList.contains('app')) {
                    event.target.classList.add("app-active");
                } else {
                    event.target.parentElement.classList.add("app-active");
                }
            },
            touchEnd(event) {
                if (event.target.classList.contains('app')) {
                    event.target.classList.remove("app-active");
                } else {
                    event.target.parentElement.classList.remove("app-active");
                }
            },
            touchMove(event) {
                if (event.touches) {
                    let x = event.touches[0].pageX - window.pageXOffset;
                    let y = event.touches[0].pageY - window.pageYOffset;

                    let target = document.elementFromPoint(x, y);

                    if (target.innerHTML !== event.target.innerHTML && target.innerHTML !== this.$el.innerHTML) {
                        if (event.target.classList.contains('app')) {
                            event.target.classList.remove("app-active");
                        } else {
                            event.target.parentElement.classList.remove("app-active");
                        }
                    }
                } else {
                    if (event.target.classList.contains('app')) {
                        event.target.classList.remove("app-active");
                    } else {
                        event.target.parentElement.classList.remove("app-active");
                    }
                }
            }
        }
    }
</script>

<style scoped>
    @import '/client-resources.css';

    #home {
        background-color: var(--home-main-background-color);
        font-size: var(--home-main-font-size);
        -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
        width: 100%;
        height: 100%;
    }

    .header {
        width: 100vw;
        height: var(--app-back-size);
        padding-left: var(--back-button-left);
        padding-top: var(--back-button-top);
        display: grid;
        align-items: center;
        grid-template-columns: calc(var(--app-back-size) + 10px) 1fr;
        margin-bottom: calc(var(--home-buttons-top) - var(--app-back-size) - var(--back-button-top));
    }

    .header h1 {
        margin: 0;
        grid-row: 1;
        font-size: 37px;
    }

    .back {
        position: fixed;
        top: 0;
        background: -webkit-gradient(linear, 0 0, 100% 0,
        from(rgba(0, 0, 0, 0.8)), to(rgba(0, 0, 0, 0))) left top no-repeat;
        width: var(--home-main-app-width);
        height: 100%;
        overflow-y: scroll;
        overflow-x: hidden;
        -webkit-overflow-scrolling: touch;
    }

    .buttons-container {
        width: var(--home-main-app-width);
        height: calc(100% + 1px);
    }

    .buttons {
        height: calc(100% - var(--home-buttons-top));
    }

    .faded-back {
        height: var(--home-main-faded-back-height);
        background: -webkit-gradient(linear, 0 0, var(--home-main-fade-length) 0,
        from(rgba(255, 255, 255, 0.35)), to(rgba(255, 255, 255, 0))) left no-repeat;
        line-height: var(--home-main-faded-back-height);
        padding-left: var(--back-button-left);
    }

    .hline {
        height: var(--home-main-hline-thickness);
        width: var(--home-main-hline-length);
        background: -webkit-gradient(linear, 0 0, 100% 0,
        from(rgba(255, 255, 255, 1)), to(rgba(255, 255, 255, 0))) left no-repeat;
    }

    .app {
        line-height: calc(var(--home-main-faded-back-height) * 1.5);
        height: calc(var(--home-main-faded-back-height) * 1.5);
        width: var(--home-main-fade-length);
        display: grid;
        grid-template-rows: 100%;
        align-items: center;
    }

    .app-active {
        background: -webkit-gradient(linear, 0 0, 100% 0,
        from(rgba(255, 255, 255, 0.5)), to(rgba(255, 255, 255, 0))) left no-repeat;
        background-size: 100% 100%;
    }
</style>
