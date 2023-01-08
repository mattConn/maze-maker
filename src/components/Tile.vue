<script>
// This is the Tile component.
// It is a single tile in the maze which holds two walls: west and north.
// These walls are toggled on and off by clicking on them.

    export default {
        props: {
            north: Boolean,
            west: Boolean,
            hasBorder: Boolean, // will make maze look like a grid 
        },
        methods: {
            wallClickHandler(direction) {
                this.$emit('wall-click', direction);
            }
        },
    }
</script>

<template>
    <div :class="['tile', hasBorder ? 'has-border' : null]">
        <div @click="wallClickHandler('north')" :class="['wall', 'north', north ? 'active' : null]"></div>
        <div @click="wallClickHandler('west')" :class="['wall', 'west', west ? 'active' : null]"></div>
    </div>
</template>

<style lang="scss" scoped>
// colors
$black: rgb(30, 30, 30);
$grey: rgb(201, 201, 201);
$green: rgb(82, 198, 136);
$red: #ff7777;
$white: white;

// dimensions
$tile-width: 40px;
$wall-thickness: 20;
$wall-thickness-half: calc($wall-thickness/2);

.tile {
    width: $tile-width;
    height: $tile-width;
    position: relative;

    &.has-border {
        border-top: solid 1px $grey;
        border-left: solid 1px $grey;
    }

    &:hover {
        // background-color: $grey;
    }

    .wall {
        cursor: pointer;
        transition: .1s;
        background-color: $white;
        opacity: 0;
        position: absolute;

        &.active {
            background-color: $black;
            opacity: 1;
            &:hover {
                background-color: $red;
                opacity: 1;
            }
        }

        &:hover {
            background-color: $green;
            opacity: 1;
        }


        &.west{
            width: #{$wall-thickness}px;
            height: 100%;
            &.active {
                width: #{$wall-thickness-half}px;
                &:hover {
                    width: #{$wall-thickness}px;
                }
            }
        }

        &.north{
            width: 100%; 
            height: #{$wall-thickness}px;
            top: 0;
            &.active {
                height: #{$wall-thickness-half}px;
                &:hover {
                    height: #{$wall-thickness}px;
                }
            }
        }

    }

    .west-east-row {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        height: 100%;
    }
}
</style>