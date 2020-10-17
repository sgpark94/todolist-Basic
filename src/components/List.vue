<template>
    <div>
        <v-card class="ma-3 pa-2"
            :class="{done: list.status === 'done'}"
            v-for="(list, index) in todoList"
            :key="index"
        >
            <p>{{ list.memo }}</p>
            <p>{{ list.status }}</p>
            <div>
                <v-btn
                    @click="$emit('statusControl', index, 'done')"
                    v-if="list.status === 'created'"
                    small fab flat color="indigo"
                >
                    <i class="fas fa-check"></i><!-- 완료 -->
                </v-btn>
                <v-btn
                    @click="$emit('statusControl', index, 'created')"
                    v-else
                    small fab flat color="red"
                >
                    <i class="fas fa-redo"></i><!-- 리셋 -->
                </v-btn>
                <v-btn
                    @click="$emit('listDelete', index)"
                    small fab flat color="green"
                >
                    <i class="far fa-trash-alt"></i><!-- 삭제 -->
                </v-btn>
                <v-btn
                    v-if="list.status === 'created'"
                    @click="listEdit(list.memo, index)"
                    small fab flat color="yellow"
                >
                    <i class="far fa-edit"></i><!-- 수정 -->
                </v-btn>
            </div>
        </v-card>
    </div>
</template>

<script>
import { eventBus } from "../main"
export default {
    props: ["todoList"],
    methods: {
        listEdit(memo, index){
            eventBus.listEdit(memo, index)
        }
    }
}
</script>

<style scoped>
    .done{
        background-color: rgba(0, 0, 0, .2);
    }
    .done p{
        text-decoration: line-through;
        color: rgba(0, 0, 0, .5);
    }
</style>