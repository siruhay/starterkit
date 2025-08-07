<template>
    <tr>
        <td>
            <v-checkbox-btn
                :model-value="isSelected(internalItem)"
                color="blue-grey"
                @update:model-value="toggleSelect(internalItem)"
            ></v-checkbox-btn>
        </td>

        <slot
            :headers="headers"
            :item="item"
            :index="index"
            :internalItem="internalItem"
            :isSelected="isSelected"
            :toggleSelect="toggleSelect"
        >
            <td
                v-for="(column, colIndex) in headers"
                :key="colIndex"
                @click="toggleSelect(internalItem)"
            >
                <template v-if="column.value === 'name' && 'nest_deep' in item">
                    <div
                        class="d-flex align-center"
                        :class="item.nest_deep > 0 ? 'fill-height' : ''"
                        :key="colIndex"
                    >
                        <template v-if="item.nest_deep !== -1">
                            <div
                                class="nestedset d-flex align-center fill-height"
                                v-for="(itm, idx) in item.nest_deep"
                                :key="idx"
                            >
                                <template v-if="itm < item.nest_deep">
                                    <v-divider vertical></v-divider>
                                </template>

                                <template v-if="itm === item.nest_deep">
                                    <v-divider vertical></v-divider>
                                    <v-divider class="mr-1"></v-divider>
                                </template>
                            </div>
                        </template>
                        <span class="flex-grow-1">{{
                            item[column.value]
                        }}</span>
                    </div>
                </template>

                <template v-else>
                    {{ item[column.value] }}
                </template>
            </td>
        </slot>
    </tr>
</template>

<script>
export default {
    name: "item-data",

    props: {
        headers: Array,
        item: Object,
        index: Number,
        internalItem: Object,
        isSelected: Function,
        toggleSelect: Function,
    },
};
</script>
