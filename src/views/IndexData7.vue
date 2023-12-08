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
            data:"",
            loading: true
        }
    },
    methods: {
        async getrequests() {
            const datalist = await requests.info1()
            if (datalist.data.code == 200) {

                this.loading = false
                this.data=datalist.data.data
                this.$nextTick(() => {
                    this.getdata()
                })

            }
        },
        getdata() {
            var myChart = echarts.init(this.$refs.app);
            var option;
            option = {
                title: {
                    text: 'Referer of a Website',
                    subtext: 'Fake Data',
                    left: 'center'
                },
                tooltip: {
                    trigger: 'item'
                },
                legend: {
                    orient: 'vertical',
                    left: 'left'
                },
                series: [
                    {
                        name: 'Access From',
                        type: 'pie',
                        radius: '50%',
                        data: this.data,
                        emphasis: {
                            itemStyle: {
                                shadowBlur: 10,
                                shadowOffsetX: 0,
                                shadowColor: 'rgba(0, 0, 0, 0.5)'
                            }
                        }
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