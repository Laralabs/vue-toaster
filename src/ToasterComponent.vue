<template>
    <notifications :group="group" :width="width" :position="position" :animation-type="animationType" :max="max" :reverse="reverse"></notifications>
</template>
<script>
    const Component = {
        name: 'Toaster',
        props: {
            group: {
                type: String,
                default: ''
            },
            width: {
                type: [Number, String],
                default: 300
            },
            position: {
                type: [String, Array],
                default: 'top right'
            },
            animationType: {
                type: String,
                default: 'css',
                validator (value) {
                    return value === 'css' || value === 'velocity'
                }
            },
            max: {
                type: Number,
                default: Infinity
            },
            reverse: {
                type: Boolean,
                default: false
            }
        },
        data() {
            return {
                animation: {
                    enter (element) {
                        /*
                         *  "element" - is a notification element
                         *    (before animation, meaning that you can take it's initial height, width, color, etc)
                         */
                        let height = element.clientHeight;

                        return {
                            // Animates from 0px to "height"
                            height: [height, 0],

                            // Animates from 0 to random opacity (in range between 0.5 and 1)
                            opacity: [Math.random() * 0.5 + 0.5, 0]
                        }
                    },
                    leave: {
                        height: 0,
                        opacity: 0
                    }
                },
                toaster: {
                    data: toaster.data
                }
            }
        },
        mounted() {
            if (typeof this.toaster.data === 'object') {
                Object.keys(this.toaster.data).forEach(key => {
                    let group = this.toaster.data[key];
                    for (let i = 0, len = group.messages.length; i < len; i++) {
                        let message = group.messages[i];
                        this.addMessage(message.group, message.title, message.message, message.type, message.duration, message.speed);
                    }
                });
            }
        },
        methods: {
            addMessage: function (group, title, text, type, duration, speed) {
                this.$notify({
                    group: group,
                    title: title,
                    text: text,
                    type: type,
                    duration: duration,
                    speed: speed
                })
            }
        }
    };

    export default Component
</script>