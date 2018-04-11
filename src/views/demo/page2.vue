<style lang="less">
    @import "../../styles/common.less";
</style>
<template>
    <div class="home-main">
       <Card style="width: 500px;">
            <p slot="title">待办事项</p>
            <a slot="extra" @click.prevent="addNewToDoItem"><Icon type="plus-round"></Icon>新建事项</a>
            <div v-for="(item, index) in toDoList" :key="'todo-item' + (toDoList.length - index)" class="to-do-item">
                <to-do-list-item :content="item.title"></to-do-list-item>
            </div>
       </Card>
       <Modal
            v-model="showAddNewTodo"
            title="添加新的待办事项"
            @on-ok="addNew"
            @on-cancel="cancelAdd">
            <Row type="flex" justify="center">
                <Input v-model="newToDoItemValue" icon="compose" placeholder="请输入..." style="width: 300px" />
            </Row>
            <Row slot="footer">
                <Button type="text" @click="cancelAdd">取消</Button>
                <Button type="primary" @click="addNew">确定</Button>
            </Row>
        </Modal>
    </div>
</template>

<script>
import toDoListItem from '@/components/todolist/toDoListItem.vue';

export default {
    name: 'page2',
    components: {
        toDoListItem
    },
    data () {
        return {
            toDoList: [
                {
                    title: '去iView官网学习完整的iView组件'
                },
                {
                    title: '写一个demo'
                },
                {
                    title: '熟悉api'
                },
                {
                    title: '熟练做出页面'
                }
            ],
            showAddNewTodo: false,
            newToDoItemValue: ''
        };
    },
    computed: {
       
    },
    methods: {
        addNewToDoItem(){
            this.showAddNewTodo = true;
        },
        addNew(){
            if (this.newToDoItemValue.length !== 0) {
                this.toDoList.unshift({
                    title: this.newToDoItemValue
                });
                setTimeout(() => {
                    this.newToDoItemValue = '';
                }, 200);
                this.showAddNewTodo = false;
            } else {
                this.$Message.error('请输入待办事项内容');
            }
        },
        cancelAdd(){
            this.showAddNewTodo = false;
            this.newToDoItemValue = '';
        }
    }
};
</script>
