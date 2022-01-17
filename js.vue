const vm = new Vue({
  el: "#app",
  data: {
    todoItem: {
      title: '',
      done: false
    },
    todolist: [],
    selItem: {}//存放修改数据
  },
  created(){
    let items=JSON.parse(localStorage.getItem('todolist'))
    this.todolist=items?items:[]
  },
  methods: {
    add() {
      if (this.todoItem.title) {
        this.todolist.push(this.todoItem);
        this.todoItem = { title: '', done: false }
      }
      else {
        alert('不能为空')
      }
      // 数据存储
      localStorage.setItem('todolist', JSON.stringify(this.todolist))
    },
    setDone(item) {
      item.done = true;
      localStorage.setItem('todolist', JSON.stringify(this.todolist))
    },
    setDoing(item) {
      item.done = false;
      localStorage.setItem('todolist', JSON.stringify(this.todolist))
    },
    setSel(item) {//实现修改数据
      this.selItem = item;
    },
    doUpdate() {
      this.selItem = {};
      localStorage.setItem('todolist', JSON.stringify(this.todolist))
    },
    del(item) {
      let index = this.todolist.indexOf(item);
      this.todolist.splice(index, 1);
      localStorage.setItem('todolist', JSON.stringify(this.todolist))
    },
  },
  computed: {
    doingList() {
      return this.todolist.filter((item) => {
        return !item.done;
      })
    },
    doneList() {
      return this.todolist.filter((item) => {
        return item.done;
      })
    }
  }
});