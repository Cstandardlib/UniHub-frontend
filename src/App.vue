<style scoped>
.layout{
    border: 1px solid #d7dde4;
    background: #f5f7f9;
    position: relative;
    border-radius: 4px;
    overflow: hidden;
/*
    top: 150px;
    left: 200px;
*/
}

.layout-logo{
    width: 100px;
    height: 30px;
    background: #5b6270;
    border-radius: 3px;
    float: left;
    position: relative;
    top: 15px;
    left: 20px;
}
.layout-nav{
    width: 420px;
    margin: 0 auto;
    margin-right: 20px;
    top: 150px;
    left: 200px;

}
.layout-footer-center{
    text-align: center;
}
</style>
<template>
    <div class="layout">
        <Layout>
            <Header>
                <Menu mode="horizontal" theme="dark" active-name="1">
                    <div class="layout-logo"></div>
                    <div class="layout-nav">
                        <MenuItem name="1">
                            <Icon type="ios-navigate"></Icon>
                            Item 1
                        </MenuItem>
                        <MenuItem name="2">
                            <Icon type="ios-keypad"></Icon>
                            Item 2
                        </MenuItem>
                        <MenuItem name="3">
                            <Icon type="ios-analytics"></Icon>
                            Item 3
                        </MenuItem>
                        <MenuItem name="4">
                            <Icon type="ios-paper"></Icon>
                            Item 4
                        </MenuItem>
                    </div>
                </Menu>
            </Header>
            <Layout :style="{padding: '0 50px'}">
                
                <Content :style="{padding: '24px 0', minHeight: '280px', background: '#fff'}">
                    <Layout>
                        <Sider hide-trigger :style="{background: '#fff'}">
                            <Tree :data="data"></Tree>
                            <Menu active-name="1-2" theme="light" width="auto" :open-names="['1']">
                                <Submenu name="1">
                                    <template #title>
                                        <Icon type="md-folder"></Icon>
                                        Item 1
                                    </template>
                                    <MenuItem name="1-1">Option 1</MenuItem>
                                    <MenuItem name="1-2">Option 2</MenuItem>
                                    <MenuItem name="1-3">Option 3</MenuItem>
                                    <Submenu name="1-4">
                                        <template #title>
                                            <Icon type="md-folder-open"></Icon>
                                            Item 1-4
                                        </template>
                                        <MenuItem name="1-4-1">
                                            <Icon type="md-document"></Icon>
                                            Option 1</MenuItem>
                            
                                    </Submenu>
                                </Submenu>
                                <Submenu name="2">
                                    <template #title>
                                        <Icon type="ios-keypad"></Icon>
                                        Item 2
                                    </template>
                                    <MenuItem name="2-1">Option 1</MenuItem>
                                    <MenuItem name="2-2">Option 2</MenuItem>
                                </Submenu>
                                <Submenu name="3">
                                    <template #title>
                                        <Icon type="ios-analytics"></Icon>
                                        Item 3
                                    </template>
                                    <MenuItem name="3-1">Option 1</MenuItem>
                                    <MenuItem name="3-2">Option 2</MenuItem>
                                </Submenu>
                            </Menu>
                        </Sider>
                        <Content :style="{padding: '24px', minHeight: '280px', background: '#fff'}">
                            <Breadcrumb :style="{margin: '16px 0'}">
                                <BreadcrumbItem>Home</BreadcrumbItem>
                                <BreadcrumbItem>Components</BreadcrumbItem>
                                <BreadcrumbItem>Layout</BreadcrumbItem>
                            </Breadcrumb>
                            <!--:model-value="previewData" v-model="newValue"-->
                            <v-md-editor :style="{top: '150px', left: '240px' }"
                                :placeholder="placeholder"
                                :disabled-menus="[]"
                                
                                v-model="text"
                                :height="height"
                                @change="handleChange">
                            </v-md-editor>
                        </Content>
                    </Layout>
                </Content>
            </Layout>
            <Footer class="layout-footer-center">2023 &copy; Unihub::Ultimate</Footer>
        </Layout>
    </div>
<!--
    <Form ref="formInline" :model="formInline" :rules="ruleInline" 
    label-position="right" :label-width="50" inline>
        <FormItem prop="user">
            <Input type="text" v-model="formInline.user" placeholder="Username">
                <template #prepend>
                <Icon type="ios-person-outline"></Icon>
                </template>
            </Input>
        </FormItem>
        <FormItem prop="password">
            <Input type="password" v-model="formInline.password" placeholder="Password">
                <template #prepend>
                <Icon type="ios-lock-outline"></Icon>
                </template>
            </Input>
        </FormItem>
        <FormItem>
            <Button type="primary" @click="handleSubmit('formInline')">Signin</Button>
        </FormItem>
    </Form>
-->
</template>

<script>
    export default {
        data () {
            return {
                text: 'Hello, World! \n ![Pku logo](https://vim.pku.edu.cn/images/content/2017-10/20171027165035344238.jpg)',
                isCollapsed: false
                ,
                formInline: {
                    user: '',
                    password: ''
                },
                ruleInline: {
                    user: [
                        { required: true, message: 'Please fill in the user name', trigger: 'blur' }
                    ],
                    password: [
                        { required: true, message: 'Please fill in the password.', trigger: 'blur' },
                        { type: 'string', min: 6, message: 'The password length cannot be less than 6 bits', trigger: 'blur' }
                    ]
                },
                data: [
                    {
                        title: 'parent 1',
                        expand: true,
                        children: [
                            {
                                title: 'parent 1-1',
                                expand: true,
                                children: [
                                    {
                                        title: 'leaf 1-1-1'
                                    },
                                    {
                                        title: 'leaf 1-1-2'
                                    }
                                ]
                            },
                            {
                                title: 'parent 1-2',
                                expand: true,
                                children: [
                                    {
                                        title: 'leaf 1-2-1'
                                    },
                                    {
                                        title: 'leaf 1-2-1'
                                    }
                                ]
                            }
                        ]
                    }
                ]
            };
        },
        computed: {
            menuitemClasses: function () {
                return [
                    'menu-item',
                    this.isCollapsed ? 'collapsed-menu' : ''
                ]
            }
        },
        methods: {
            handleSubmit(name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        this.$Message.success('Success!');
                    } else {
                        this.$Message.error('Fail!');
                    }
                })
            }
        }
    }
</script>

