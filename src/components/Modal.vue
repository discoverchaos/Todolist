<template lang="pug">
Transition(name="modal")
    .modal(@click="$emit('showOrClose'), $emit('editFalse')")
        .modal-block(@click.stop) 
            h2 {{ edit ? 'Изменить' : 'Добавить' }} заметку
            form(action="" @submit.prevent="send").modal-inputs
                input(type="text", placeholder="Title" v-model="user.title" required)
                textarea(placeholder="Content" v-model="user.text" required)
                .modal-btns
                    button(type="button" @click="$emit('showOrClose'), $emit('editFalse')") Отмена
                    button(v-if="!edit") Добавить
                    button(type="button" v-else @click="changeNote") Изменить
</template>
<script>
export default {
  props: {
    edit: Boolean,
    curNote: Object,
    currentId: Number
  },
    data(){
        return {
            user: {title: '', text: '', id: this.currentId}
        }
    },
    methods: {
        send(){
            this.$emit('addNote', {...this.user})
            this.$emit('showOrClose')
            this.user.title = '', this.user.text = '', this.user.id = localStorage.id++
            
        },
        changeNote(){
          if(this.user.title != '' && this.user.text != ''){
            const editedNote = {
              id: this.curNote.id,
              title: this.user.title,
              text: this.user.text,
              date: 'Изменено ' + new Date().toLocaleString()
            }
            this.$emit('editedNote', editedNote)
            this.user.title = ''
            this.user.text = ''
          }
        }
        
    },
};
</script>
<style lang="scss">
.modal {
  background: rgba(0, 0, 0, 0.35);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  &-block {
    background: linear-gradient(
        0deg,
        rgba(103, 80, 164, 0.11),
        rgba(103, 80, 164, 0.11)
      ),
      #fffbfe;
    border-radius: 28px;
    padding: 24px;
    width: 312px;
    display: flex;
    flex-direction: column;
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3),
      0px 1px 3px 1px rgba(0, 0, 0, 0.15);
    h2 {
      margin-bottom: 16px;
      line-height: 32px;
      color: #1c1b1f;
    }
    input,
    textarea {
      width: 264px;
      display: flex;
      align-items: center;
      padding: 8px 16px 9px;
      resize: none;
      border: none;
      outline: none;
      height: 40px;
      background: #e7e0ec;
      border-radius: 4px 4px 0px 0px;
      margin-bottom: 16px;
      border-bottom: 1px solid #1c1b1f;
      &::placeholder {
        color: #6750a4;
        font-size: 12px;
        line-height: 16px;
        letter-spacing: 0.4px;
        opacity: 0.8;
      }
    }
  }
  &-btns {
    display: flex;
    justify-content: flex-end;
    gap: 32px;
    margin-top: 18px;
    button {
      cursor: pointer;
      font-family: RM;
      color: #cf1b1b;
      text-transform: uppercase;
      letter-spacing: 0.1px;
      font-size: 14px;
      background: none;
      outline: none;
      border: none;
      &:last-child {
        color: #6750a4;
      }
    }
  }
}
.modal-enter-active,
.modal-leave-active {
  transition: 0.3s linear;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.2);
}
</style>