<template>
<div class="box">
    <table class="table table-hover table-bordered">
        <thead>
            <!--<tr>
                <th width="10%">id</th>
                <th width="30%">name</th>
                <th width="40%">content</th>
                <th width="20%">remark</th>
            </tr>-->
            
			<tr>
				<th style="width: 8px;"><input type="checkbox"
					class="group-checkable" data-set="#sample_1 .checkboxes" /></th>
				<th>用户名</th>
				<th>真实姓名</th>
				<th>邮箱</th>
				<th>手机号</th>
				<th>最近登录时间</th>
				<th>登录失败次数</th>
				<th>备注</th>
				<th>账户是否可用</th>
				<th>操作</th>
			</tr>
        </thead>
        <tbody>
            <!--<tr v-for="data in tableList">
                <td v-text="data.num"></td>
                <td v-text="data.author"></td>
                <td v-text="data.contents"></td>
                <td v-text="data.remark"></td>
            </tr>-->
			<tr class="odd gradeX" v-for="item in tableList" track-by="$index">
				<td><input type="checkbox" class="checkboxes" value="1" /></td>
				<td style="display: none;">{{ item.id}}</td>
				<td>{{ item.userName}}</td>
				<td>{{ item.realName}}</td>
				<td>{{ item.email}}</td>
				<td>{{ item.mobilePhone}}</td>
				<td>{{ item.lastLoginTime}}</td>
				<td>{{ item.lastLoginFailCount}}</td>
				<td>{{ item.memo}}</td>
				<td>{{ item.isAvailable==1?'可用':'不可用'}}</td>
				<td>
					<button type="button" class="btn blue submitButton">
						<i class="fa fa-save"></i>修改
					</button>
					<button type="button" class="btn blue submitButton">
						<i class="fa fa-save"></i>删除
					</button>
				</td>
			</tr>
        </tbody>
        <tfoot>
            <tr>
                <td colspan="20">
                    <div class="pull-left">
                        <button class="btn btn-default" @click="refresh">刷新</button>
                    </div>
                    <div class="pull-right">
                        <!--<boot-page v-ref:page :async="false" :data="lists" :lens="lenArr" :page-len="pageLen" :param="param"></boot-page>-->
                        <boot-page v-ref:page :async="true" :lens="lenArr" :url="url" :page-len="pageLen" :param="param"></boot-page>
                    	<!--url为服务器请求地址，param需要向服务器发送的参数对象-->
                    </div>
                    </div>
                </td>
            </tr>
        </tfoot>
    </table>
</div>
</template>

<!--<script>
//import bootPage from './components/BootPage.vue'
//
//export default {
//  data () {
//      return {
//          lenArr: [5, 50, 100], // 每页显示长度设置
//          pageLen: 5, // 可显示的分页数
//          // url: '/bootpage/', // 请求路径
//          param: {}, // 传递参数
//          lists: [
//              {num: 1, author: 'luozh', contents: 'BootPage是一款支持静态数据和服务器数据的表格分页组件', remark: 'dsds'},
//              {num: 2, author: 'luozh', contents: '支持调整每页显示行数和页码显示个数，样式基于bootstrap', remark: 'dsds'},
//              {num: 3, author: 'luozh', contents: '<boot-page>标签中async指是否从服务器端获取数据，false为否', remark: 'dsds'},
//              {num: 4, author: 'luozh', contents: 'data为静态的表格数据数组；', remark: 'dsds'},
//              {num: 5, author: 'luozh', contents: 'lens为每页显示行数的数组', remark: 'dsds'},
//              {num: 6, author: 'luozh', contents: 'page-len为可显示的页码数', remark: 'dsds'},
//              {num: 7, author: 'luozh', contents: '服务器回传参数为{data:[], page_num: 6}, 其中data为表格数据，page_num为总页数', remark: 'dsds'},
//              {num: 8, author: 'luozh', contents: '可以调用this.$refs.page.refresh()刷新表格数据', remark: 'dsds'}
//          ], // 表格原始数据
//  		lists:[
//	    		{"first_task_count":4,"total_member_count":1,"first_task_money":41.49,"sec_task_money":0.0,"thr_task_count":0,"total_task_money":41.49,"sec_member_count":0,"total_task_count":4,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":1},
//	    		{"total_member_count":51,"sec_member_count":0,"my_code":"3116","invitation_uid":5,"first_task_count":4,"first_task_money":29.26,"phone":"15888780307","nickname":"淡忘","sec_task_money":0.0,"thr_task_count":0,"total_task_money":29.26,"total_task_count":4,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":51},
//	    		{"total_member_count":52,"sec_member_count":0,"my_code":"3122","invitation_uid":11,"first_task_count":10,"first_task_money":24.4,"phone":"15268585613","nickname":"马景聿","sec_task_money":0.0,"thr_task_count":0,"total_task_money":24.4,"total_task_count":10,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":52},
//	    		{"total_member_count":30,"sec_member_count":0,"my_code":"XM2305","invitation_uid":2305,"first_task_count":3,"first_task_money":17.07,"phone":"15858115561","nickname":"陈荣","sec_task_money":0.0,"thr_task_count":0,"total_task_money":17.07,"total_task_count":3,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":30},
//	    		{"total_member_count":63,"sec_member_count":0,"my_code":"3130","invitation_uid":19,"first_task_count":6,"first_task_money":14.64,"phone":"17306468286","nickname":"张俊","sec_task_money":0.0,"thr_task_count":0,"total_task_money":14.64,"total_task_count":6,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":63},
//	    		{"total_member_count":29,"sec_member_count":0,"my_code":"3125","invitation_uid":14,"first_task_count":2,"first_task_money":14.63,"phone":"15158170790","nickname":"王京","sec_task_money":0.0,"thr_task_count":0,"total_task_money":14.63,"total_task_count":2,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":29},
//	    		{"total_member_count":137,"sec_member_count":0,"my_code":"3118","invitation_uid":7,"first_task_count":5,"first_task_money":12.2,"phone":"15826988192","nickname":"Ares、","sec_task_money":0.0,"thr_task_count":0,"total_task_money":12.2,"total_task_count":5,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":137},
//	    		{"total_member_count":51,"sec_member_count":0,"my_code":"3117","invitation_uid":6,"first_task_count":1,"first_task_money":11.25,"phone":"13326136307","nickname":"毛新","sec_task_money":0.0,"thr_task_count":0,"total_task_money":11.25,"total_task_count":1,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":51},
//	    		{"total_member_count":36,"sec_member_count":0,"my_code":"3114","invitation_uid":3,"first_task_count":4,"first_task_money":9.76,"phone":"18268874030","nickname":"邵飞","sec_task_money":0.0,"thr_task_count":0,"total_task_money":9.76,"total_task_count":4,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":36},
//	    		{"total_member_count":35,"sec_member_count":0,"my_code":"3115","invitation_uid":4,"first_task_count":3,"first_task_money":7.32,"phone":"15858175832","nickname":"＃般若波羅蜜多心經＃","sec_task_money":0.0,"thr_task_count":0,"total_task_money":7.32,"total_task_count":3,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":35},
//	    		{"total_member_count":49,"sec_member_count":0,"my_code":"3113","invitation_uid":2,"first_task_count":3,"first_task_money":7.32,"phone":"13866082892","nickname":"A丿ヽoo年轻丶","sec_task_money":0.0,"thr_task_count":0,"total_task_money":7.32,"total_task_count":3,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":49},
//	    		{"total_member_count":76,"sec_member_count":0,"my_code":"3120","invitation_uid":9,"first_task_count":1,"first_task_money":7.31,"phone":"13666628220","nickname":"王泽鑫","sec_task_money":0.0,"thr_task_count":0,"total_task_money":7.31,"total_task_count":1,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":76},
//	    		{"total_member_count":23,"sec_member_count":0,"my_code":"3133","invitation_uid":22,"first_task_count":1,"first_task_money":2.44,"phone":"13819465014","nickname":"叶欢","sec_task_money":0.0,"thr_task_count":0,"total_task_money":2.44,"total_task_count":1,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":23},
//	    		{"total_member_count":13,"sec_member_count":0,"my_code":"XM2122","invitation_uid":2122,"first_task_count":0,"first_task_money":0.0,"phone":"13429115720","nickname":"王海东","sec_task_money":0.0,"thr_task_count":0,"total_task_money":0.0,"total_task_count":0,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":13},
//	    		{"total_member_count":29,"sec_member_count":0,"my_code":"3137","invitation_uid":26,"first_task_count":0,"first_task_money":0.0,"phone":"15869035632","nickname":"张琴栋","sec_task_money":0.0,"thr_task_count":0,"total_task_money":0.0,"total_task_count":0,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":29},
//	    		{"total_member_count":7,"sec_member_count":0,"my_code":"3121","invitation_uid":10,"first_task_count":0,"first_task_money":0.0,"phone":"18814832792","nickname":"离落","sec_task_money":0.0,"thr_task_count":0,"total_task_money":0.0,"total_task_count":0,"sec_task_count":0,"thr_task_money":0.0,"thr_member_count":0,"first_member_count":7}
//  		],  
//  		lists:[],
//          tableList: [] // 分页组件传回的分页后数据
//      }
//  },
//  components: {
//      bootPage
//  },
//  methods: {
//      refresh () {
//          //this.$refs.page.refresh();
//          this.tableList = lists
//          this.$refs.page.refresh();
//      }
//  },
//  events: {
//
//      // 分页组件传回的表格数据
//      'data' (data) {
//          this.tableList = data
//      },
//
//      // 刷新数据
//      'refresh' () {
//          this.refresh()
//      }
//  }
//}
</script>-->

<script>
import bootPage from './components/BootPage.vue'

export default {
    data () {
        return {
            lenArr: [5, 50, 100], // 每页显示长度设置
            pageLen: 5, // 可显示的分页数
//          url: '/bootpage/', // 请求路径
            url: 'http://192.168.1.173:8080/xm-web-sys/sysUser',
            param: {}, // 传递参数
            tableList: [] // 分页组件传回的分页后数据
        }
    },
    methods: {
        refresh () {
            this.$refs.page.refresh(); //这里提供了一个表格刷新功能
        }
    },
    components: {
        bootPage
    },
    events: {

        // 分页组件传回的表格数据（这里即为服务器传回的数据）
        'data' (data) {
            this.tableList = data.data
//        console.log(JSON.stringify(this.tableList));
        },

        // 刷新数据
        'refresh' () {
            this.refresh()
        }
    }
}
</script>


<style>
@import url('./assets/css/bootstrap.min.css');

.box {
    padding: 100px;
}
</style>

