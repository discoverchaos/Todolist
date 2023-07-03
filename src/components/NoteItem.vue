<template lang="pug">
.notes-item
    .notes-item-top(:class="{between: !grid}")
        h3 {{ note.title }}
        p {{ note.date }}
    p {{ note.text }}
    .notes-item-btns
        button(@click="$emit('changeNote', note.id)")
            img(src="../assets/img/edit.svg", alt="alt")
            span РЕДАКТИРОВАТЬ
        button(@click="$emit('delNote', note.id)")
            img(src="../assets/img/trash.svg", alt="alt")
            span УДАЛИТЬ
</template>
<script>
export default {
    props: {
        grid: Boolean,
        note: Object
    }
}
</script>
<style lang="scss">
    .notes-item {
        background: linear-gradient(0deg, rgba(103, 80, 164, 0.05), rgba(103, 80, 164, 0.05)), #FFFBFE;
        box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3), 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        border-radius: 16px;
        padding: 16px 16px 16px 16px;
        max-width: 326px;
        &-top {
            &.between {
               display: flex;
               justify-content: space-between;
                flex-wrap: wrap;
            }
            h3 {
               letter-spacing: 0.1px;
               line-height: 24px;
               color: #1C1B1F;
               font-size: 16px;
               font-family: RM;
               font-weight: 500;
                word-wrap: break-word;
            }
            p {
                font-size: 14px;
                line-height: 20px;
                letter-spacing: 0.25px;
                color: #CAC4D0;
                margin-bottom: 16.25px;
            }
        }
        > p {
            max-width: 326px;
            width: 100%;
            word-wrap: break-word;
            font-size: 14px;
            line-height: 20px;
            letter-spacing: 0.25px;
            color: #49454F;
            margin-bottom: 29px;
            font-weight: 400;
            padding-right: 30px;
        }
        &-btns {
            display: flex;
            justify-content: flex-end;
            gap: 20px;
            button {
                background: transparent;
                outline: none;
                border: none;
                cursor: pointer;
                color: #6750A4;
                letter-spacing: 0.1px;
                font-weight: 700;
                display: flex;
                align-items: center;
                gap: 11px;
                padding: 10px;
                &:last-child{
                    color: #CF1B1B;
                }
            }
        }   
    }
.notes-list.active .notes-item {
    max-width: 1140px;
}
.notes-list.active .notes-item > p, .notes-item h3 {
    max-width: 1140px;
}
</style>