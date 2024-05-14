<template>
  <div class="memo">
    <div class="act">
      <button class="btn btn-primary" @click="add()">+ 추가</button>
    </div>
    <ul>
      <li v-for="d in state.data" :key="d.id" @click="edit(d.id)">
        {{ d.content }}
      </li>
    </ul>
  </div>
</template>
<script>
import { reactive } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const state = reactive({
      data: [],
    });
    const add = () => {
      const content = prompt('내용 입력');
      if (!content) {
        alert('내용 입력해줘');
        return add();
      }
      // state.data.push('추가된 메모');
      axios.post('/api/memos', { content }).then((res) => {
        // console.log(res.data);
        state.data = res.data;
      });
    };

    const edit = (id) => {
      const content = prompt(
        '내용 입력',
        state.data.find((d) => d.id === id).content
      );
      if (content) {
        // console.log(content);
        axios.put('/api/memos/' + id, { content }).then((res) => {
          state.data = res.data;
        });
      }
    };

    axios.get('/api/memos').then((res) => {
      state.data = res.data;
    });

    return { state, add, edit };
  },
};
</script>
<style scoped>
.memo {
  .act {
    padding: 8px 12px;
    text-align: right;
  }
  ul {
    border-top: 1px solid #ddd;
    list-style: none;
    padding: 0;
    margin: 0;
    li {
      padding: 16px;
      color: goldenrod;
      border: 1px solid #eee;
      &:first-child {
        border-top: 0;
      }
    }
  }
}
</style>
