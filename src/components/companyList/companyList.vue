<template>
    <JobList :title="title" :jobList="jobList" />
</template>


<script>
import JobList from "../ListJob/JobList.vue"
import axios from "../axios"
export default {
    components: {
        JobList,
    },
    data() {
        return {
            title: "Quick Links",
            jobList: []
        }
    },

    mounted() {
        axios.get("http://54.169.143.212/api/companyName").then((res) => {
            this.jobList = []
            for (let value of res.data) {
                this.jobList.push(value.company_name)
            }
        })
    }
}

</script>