<template>
    <div>
        <v-row>{{course.name}}</v-row>
        <v-row>
            <v-col>课程编号</v-col><v-col>{{this.course.course_id}}</v-col>
        </v-row>
        <v-row>
            <v-col>课程类别</v-col>
            <v-col>
                <div v-if="this.course.main_class===1">专业课</div>
                <div v-if="this.course.main_class===2">通选课</div>
                <div v-if="this.course.main_class===3">体育课</div>
            </v-col>
        </v-row>
        <v-row>
            <v-col>课程学分</v-col><v-col>{{this.course.credit}}</v-col>
        </v-row>
        <v-row>
            <v-col>开课院系</v-col><v-col>{{this.course.dept}}</v-col>
        </v-row>
        <v-row>
            <v-col>任课老师</v-col><v-col>{{this.course.lecturer}}</v-col>
        </v-row>
        <v-row>
            <v-col>上课地点</v-col><v-col>{{this.course.pos}}</v-col>
        </v-row>
        <v-row>
            <v-col>上课时间</v-col>
            <v-col v-for ="time in this.course.times" :key="item.day" :value="item.period">
                {{time.day}} : {{time.period}}
            </v-col>
        </v-row>
        <v-row>
            <v-col>详细描述</v-col><v-col>{{this.course.detail}}</v-col>
        </v-row>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    mounted () {
        axios.get('http://localhost:8000/courses/1233343', {}).then(response => (this.course = response.course))
    },
    data () {
        return {
            course : {
                "course_id": 1233343,   // From elective.pku.edu.cn
                // "class_no": 1,
                "name": "软件工程",
                "credit": 4,
                "main_class": 1,     // 课程类别, 专业课、通选课、体育课等
                "sub_class": null,   // 通选课类别(ABCDEF) / 英语课类别(ABCC+)，其它大类可缺省
                "times": [
                    {"day":2, "period":[3,4]},
                    {"day":4, "period":[5,6]},
                ],
                "lecturer": "孙艳春",
                "pos": "理教201",
                "dept": 48,
                "detail": "About software developing...",     // 详细的文字描述
                "elect_status": 0,    // none / pending / elected
                // "willpoint": 99, feature: 在详情页选课
            }
        }
    }
}
</script>