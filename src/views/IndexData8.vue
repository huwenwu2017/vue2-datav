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
            data: "",
            loading: true
        }
    },
    methods: {
        async getrequests() {
            const datalist = await requests.info2()
            if (datalist.data.code == 200) {

                this.loading = false
                this.data = datalist.data.data
                this.$nextTick(() => {
                    this.getdata()
                })

            }
        },
        getdata() {
            var myChart = echarts.init(this.$refs.app);
            var option;
            option = {
                tooltip: {
                    trigger: 'item'
                },
                legend: {
                    top: '5%',
                    left: 'center'
                },
                series: [
                    {
                        name: 'Access From',
                        type: 'pie',
                        radius: ['40%', '70%'],
                        avoidLabelOverlap: false,
                        label: {
                            show: false,
                            position: 'center'
                        },
                        emphasis: {
                            label: {
                                show: true,
                                fontSize: 40,
                                fontWeight: 'bold'
                            }
                        },
                        labelLine: {
                            show: false
                        },
                        data: this.data
                    }
                ]
            };
            option && myChart.setOption(option);
        }
    },
    mounted() {
        setInterval(() => {
            this.getrequests()
        }, 60000)
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