<template>
    <div class="box">
        <dv-loading style="color: aqua;" v-if="loading">加载中</dv-loading>
        <div ref="app" class="echarts" v-else></div>
    </div>
</template>
<script>
import * as echarts from 'echarts';
import * as requests from "./api/index"
export default {
    data() {
        return {
            xdata: "",
            ydata: "",
            loading: true
        }
    },
    methods: {
        async getrequests() {
            const datalist = await requests.info()
            if (datalist.data.code == 200) {

                this.loading = false

                this.xdata = Object.keys(datalist.data.data)
                this.ydata = Object.values(datalist.data.data)

                this.$nextTick(() => {
                    this.getdata()
                })

            }
        },
        getdata() {
            var myChart = echarts.init(this.$refs.app);
            var option;
            option = {
                xAxis: {
                    type: 'category',
                    data: this.xdata
                },
                yAxis: {
                    type: 'value'
                },
                series: [
                    {
                        data: this.ydata,
                        type: 'line'
                    }
                ]
            };
            option && myChart.setOption(option);
        }
    },
    mounted() {
        setInterval(() => { 
            this.getrequests() }, 60000)
        this.getrequests()
    }

}
</script>
<style scoped>
.box {
    width: 100%;
    height: 100%;

}

.echarts {
    width: 100%;
    height: 340px
}
</style>