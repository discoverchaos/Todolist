<template lang="pug">
section.notes
    .container
        .notes-top
            h2(v-if="search == ''") {{ notes.length <= 0 ? words.noinfobar[lang] : words.infobar[lang] }}
            h2(v-else) {{ words.appbarseacrch[lang] }}
            button(@click="grid = !grid")
                img(src="../assets/img/list.svg", alt="" v-if="grid")
                img(src="../assets/img/grid.svg", alt="" v-else)
                span {{grid ? 'Список' : 'Сетка'}}
        .notes-list(:class="{active: !grid}")
            NoteItem(
                :grid="grid"
                v-for="note in notes" :key="note.id"
                :note="note"
                @delNote="$emit('delNote', note.id)"
                @changeNote="$emit('changeNote', note.id)"
            )
</template>
<script>
import NoteItem from '@/components/NoteItem.vue'
export default {
    components: {NoteItem},
    props: {
        notes:{
            typeof: Array,
            required: true
        },
        lang: String,
        search: String
    },
    inject: ['words'],
    data() {
        return {
            grid: true
        }
    },
}
</script>
<style lang="scss">
    .notes {
        margin-top: 30px;
        &-top{
            margin-bottom: 30px;
            display: flex;
            justify-content: space-between;
            h2{
                font-weight: 400;
                font-size: 22px;
                user-select: none;
            }
            button {
                display: flex;
                align-items: center;
                justify-content: center;
                padding: 21px 20px;
                color: #6750A4;
                background: linear-gradient(0deg, rgba(103, 80, 164, 0.11), rgba(103, 80, 164, 0.11)), #FFFBFE;
                box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15), 0px 1px 3px rgba(0, 0, 0, 0.3);
                border-radius: 16px;
                width: 121px;
                height: 56px;
                border: none;
                outline: none;
                gap: 15px;
                span {
                    font-family: RM;
                    font-size: 14px;
                }
            }
        }
    &-list {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 24px;
        &.active {
            grid-template-columns: 1fr;     
        }
    }
    }
    .notes-list.active .notes-item{
        max-width: none;
    }
</style>