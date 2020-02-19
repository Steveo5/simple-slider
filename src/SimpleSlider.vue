<template>
    <div class="simple-slider">
        <div class="selector-container">
            <div class="selector">
                <div class="selector-prev" v-if="selectedImageIndex !== 0" @click="selectedImageIndex--">
                    <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="arrow-alt-circle-up" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="svg-inline--fa fa-arrow-alt-circle-up fa-w-16 text-secondary"><path fill="currentColor" d="M8 256C8 119 119 8 256 8s248 111 248 248-111 248-248 248S8 393 8 256zm292 116V256h70.9c10.7 0 16.1-13 8.5-20.5L264.5 121.2c-4.7-4.7-12.2-4.7-16.9 0l-115 114.3c-7.6 7.6-2.2 20.5 8.5 20.5H212v116c0 6.6 5.4 12 12 12h64c6.6 0 12-5.4 12-12z" class=""></path></svg>
                </div>
                <div class="selector-images-container">
                    <div class="selector-images" :style="selectedTransform">
                        <div class="selector-image"
                             :class="{'selected' : index === selectedImageIndex}"
                             v-for="(image, index) in images"
                             :key="image.id">
                            <div :style="'background-image: url(' + image.url + ');'"></div>
                        </div>
                    </div>
                </div>
                <div class="selector-next" v-if="selectedImageIndex !== images.length - 1" @click="selectedImageIndex++">
                    <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="arrow-alt-circle-down" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="svg-inline--fa fa-arrow-alt-circle-down fa-w-16"><path fill="currentColor" d="M504 256c0 137-111 248-248 248S8 393 8 256 119 8 256 8s248 111 248 248zM212 140v116h-70.9c-10.7 0-16.1 13-8.5 20.5l114.9 114.3c4.7 4.7 12.2 4.7 16.9 0l114.9-114.3c7.6-7.6 2.2-20.5-8.5-20.5H300V140c0-6.6-5.4-12-12-12h-64c-6.6 0-12 5.4-12 12z" class=""></path></svg>
                </div>
            </div>
        </div>
        <div class="selected-outer">
            <div class="selected-container">
                <transition name="fade"
                            v-for="(image, index) in images"
                            :key="image.id">
                    <div class="selected-image"
                         :style="'background-image: url(' + image.url+ ');'"
                         v-if="index === selectedImageIndex"></div>
                </transition>
            </div>

            <h4 v-if="images[selectedImageIndex].title">{{ images[selectedImageIndex].title }}</h4>
            <p v-if="images[selectedImageIndex].text">{{ images[selectedImageIndex].text }}</p>
        </div>
    </div>
</template>

<style lang="scss">

    .simple-slider {
        max-width: 900px;

        .fade-enter-active, .fade-leave-active {
            transition: opacity .5s;
        }
        .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
            opacity: 0;
        }

        .selected-outer {
            flex-grow: 1;

            p {
                font-size: 14px;
                color: #313131;
                margin: 10px 0;
            }

            h4 {
                font-size: 18px;
                font-weight: 500;
                letter-spacing: 1.1px;
                text-transform: uppercase;
            }

            p,
            h4 {
                font-family: Verdana, Arial,serif;
            }
        }

        .selected-container {
            padding-top: 55%;
            overflow: hidden;
            position: relative;
            flex-grow: 1;
            background-color: lightgray;

            .selected-image {
                position: absolute;
                top: 0;
                background: no-repeat center;
                background-size: cover;
                min-height: 100%;
                width: 100%;
            }
        }

        .selector-prev,
        .selector-next {
            width: 38px;
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            z-index: 1;
            background-color: white;

            svg {
                transition: transform 0.3s;
                cursor: pointer;

                &:hover {
                    transform: scale(1.2);
                }
            }
        }

        .selector-prev {
            left: -33px;
            transform: rotate(270deg);
            transform-origin: top;
        }

        .selector-next {
            right: 0;
            transform: rotate(270deg);
            transform-origin: top;
        }

        .selector-images {
            transition: transform 0.3s;
            display: flex;
        }

        .selector-container {
            display: flex;
            justify-content: center;
            padding-bottom: 20px;
        }

        .selector {
            border: 1px solid #dee2e6;
            padding: 1rem 3rem;
            position: relative;
            background-color: white;
            display: inline-block;

            .selector-images-container {
                overflow: hidden;
                max-height: 228px;
                max-width: 228px;
            }

            .selector-image {
                width: 60px;
                min-width: 60px;
                height: 60px;
                position: relative;
                margin: 0 8px;
                transition: opacity 0.3s;

                &:not(.selected) {
                    opacity: 0.2;
                }

                div {
                    position: absolute;
                    top: 0;
                    width: 100%;
                    height: 100%;
                    background: no-repeat center;
                    background-size: cover;
                }
            }
        }

        @media (min-width: 768px) {
            display: flex;

            .selector-images {
                display: block;
            }

            .selector-container {
                display: block;
                justify-content: center;
                padding-bottom: 0;
            }

            .selector-prev,
            .selector-next {
                left: 50%;
                transform: translate(-50%, 0);
                top: unset;
            }

            .selector-prev {
                top: -17px;
            }

            .selector-next {
                bottom: -22px;
            }

            .selector {
                padding: 3rem 1rem;
                display: block;
                margin-right: 32px;

                .selector-image {
                    margin: 12px 0;
                }
            }
        }
    }
</style>

<script>
    export default {
        data() {
            return {
                selectedImageIndex: 0,
                windowWidth: window.innerWidth
            }
        },
        props: {
            images: {
                type: Array,
                required: false,
                default: () => { return [
                    {
                        title: 'Image 1',
                        url: 'https://i.picsum.photos/id/848/600/400.jpg',
                        id: 1
                    },
                    {
                        title: 'Image 2',
                        url: 'https://i.picsum.photos/id/849/600/400.jpg',
                        id: 2,
                        text: 'Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry\'s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.'
                    },
                    {
                        title: 'Image 3',
                        url: 'https://i.picsum.photos/id/847/600/400.jpg',
                        id: 3
                    },
                    {
                        title: 'Image 1',
                        url: 'https://i.picsum.photos/id/848/600/400.jpg',
                        id: 4
                    },
                ] }
            },
            interval: {
                type: Number,
                required: false,
                default: -1
            },
        },
        mounted() {
            if (this.interval > 0) {
                setInterval(() => {
                    this.nextImage();
                }, this.interval)
            }

            window.onresize = () => {
                this.windowWidth = window.innerWidth
            }
        },
        methods: {
            nextImage() {
                this.selectedImageIndex++;

                if (this.selectedImageIndex >= this.images.length) {
                    this.selectedImageIndex = 0;
                }
            }
        },
        computed: {
            selectedTransform() {
                let initialTransform = 60;
                initialTransform += (this.selectedImageIndex - 2) * 12;

                if (initialTransform > 60) {
                    if (this.windowWidth > 768) {
                        return 'transform: translateY(' + -initialTransform + 'px);'
                    } else {
                        return 'transform: translateX(' + -initialTransform + 'px);'
                    }
                } else {
                    return 0;
                }
            }
        }
    }
</script>