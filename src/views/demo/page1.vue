<style lang="less">
    @import "../../styles/common.less";
</style>
<template>

    <div class="home-main">
        <Row>
            <Col span="24">
                <Row>
                    <Input v-model="orderIdInput" placeholder="请输入姓名搜搜..." style="width: 200px" />
                    <RadioGroup v-model="phone">
                        <Radio label="apple">
                            <Icon type="social-apple"></Icon>
                            <span>Apple</span>
                        </Radio>
                        <Radio label="android">
                            <Icon type="social-android"></Icon>
                            <span>Android</span>
                        </Radio>
                        <Radio label="windows">
                            <Icon type="social-windows"></Icon>
                            <span>Windows</span>
                        </Radio>
                    </RadioGroup>
                    <DatePicker type="date" placeholder="Select date" style="width: 200px"></DatePicker>
                    <Button @click="orderSearch" type="primary" icon="search">搜索</Button>
                    <Button @click="cancelSearch" type="ghost" >取消</Button>
                </Row>
            </Col>
        </Row>
        
        <Row :gutter="10" style="margin-top: 30px;">
            <Col span="22">
                <can-edit-table 
                    refs="table4" 
                    v-model="tbody" 
                    @on-change="handleChange"  
                    :columns-list="thead"
                ></can-edit-table>
            </Col>
        </Row>
       
    </div>
</template>

<script>
    import canEditTable from '@/components/table/canEditTable.vue';
    import axios from 'axios';

    const getTabledataMockUrl = 'http://api.eshengeshu.com/mock/5c3c68e3e877f5f5.json';

    export default {
        name: 'page1',
        components: {
            canEditTable,
        },
        data() {
            return {
                orderIdInput: '',
                thead: [],
                tbody: [],
                phone: 'apple'
            };
        },
        computed: {
    
        },
        methods: {
            orderSearch(){
                this.$Message.success("你点了搜索，" + this.orderIdInput);
                axios.get(getTabledataMockUrl)
                    .then(res => {
                        let _res = res.data;
                        if(_res.status == 1){
                            console.log(_res.data)
                            this.thead = _res.data.thead;
                            this.tbody = _res.data.tbody;
                        }
                    })
                    .then(res => {
                        console.log(this.thead)
                    })
            },
            cancelSearch() {
                this.$Modal.confirm({
                    title: '确定要取消吗',
                    content: '输入框内容为：' + this.orderIdInput + "<br>您刚点了取消，确定取消吗？",
                    okText: '我确定',
                    cancelText: '点错了',
                    onOk: () => {
                        this.$Message.info('您点了我确定');
                    },
                    onCancel: () => {
                        this.$Message.info('您点了点错了');
                    }
                });
            },
            handleDel (val, index) {
                this.$Message.success('删除了第' + (index + 1) + '行数据');
            },
            handleChange (val, index) {
                this.$Message.success('修改了第' + (index + 1) + '行数据');
                console.log(val)
            }
        }
    };
</script>
