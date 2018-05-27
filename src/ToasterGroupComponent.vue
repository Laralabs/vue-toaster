<template>
    <notifications :group="group" :width="width" :position="position" :animation-type="animationType" :max="max" :reverse="reverse"></notifications>
</template>
<script>
    const Component = {
        name: 'ToasterGroup',
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
        }
    };

    export default Component
</script>