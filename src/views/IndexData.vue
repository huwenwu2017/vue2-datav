<template>
    <!-- 全屏容器 -->
    <dv-full-screen-container style="background-color:black">
        <dv-border-box-11 title="香蕉麻花皮演示" >
            <!-- 我这里将页面分为上中下三块，这是第一块 -->
            <div class="box">
                <!-- 在里面在分成左中右3块 -->
                <div class="box1" style="padding-top: 40px;">
                    <dv-border-box-12>
                        <IndexData1 />
                    </dv-border-box-12>
                </div>
                <div class="box1" style="padding-top: 40px;">
                    <dv-border-box-2>
                        <IndexData2 />
                    </dv-border-box-2>
                </div>
                <div class="box1" style="padding-top: 40px;">
                    <dv-border-box-10>
                        <IndexData3 />
                    </dv-border-box-10>
                </div>
            </div>
            <!-- 第二块 -->
            <div class="box">
                <!-- 在里面在分成左中右3块 -->
                <div class="box1">
                    <dv-border-box-9>
                        <IndexData4 />
                    </dv-border-box-9>
                </div>
                <div class="box1">
                    <dv-border-box-8>
                        <IndexData5 />
                    </dv-border-box-8>
                </div>
                <div class="box1">
                    <dv-border-box-7>
                        <IndexData6 />
                    </dv-border-box-7>
                </div>
            </div>
            <!-- 第三块 -->
            <div class="box">
                <!-- 在里面在分成左中右3块 -->
                <div class="box1">
                    <dv-border-box-2>
                        <IndexData7 />
                    </dv-border-box-2>
                </div>
                <div class="box1">
                    <dv-border-box-3>
                        <IndexData8 />
                    </dv-border-box-3>
                </div>
                <div class="box1">
                    <dv-border-box-8>
                        <IndexData9 />
                    </dv-border-box-8>
                </div>
            </div>
        </dv-border-box-11>
    </dv-full-screen-container>
</template>
<script>

import IndexData1 from "./IndexData1.vue"
import IndexData2 from "./IndexData2.vue"
import IndexData3 from "./IndexData3.vue"
import IndexData4 from "./IndexData4.vue"
import IndexData5 from "./IndexData5.vue"
import IndexData6 from "./IndexData6.vue"
import IndexData7 from "./IndexData7.vue"
import IndexData8 from "./IndexData8.vue"
import IndexData9 from "./IndexData9.vue"
export default {
    data() {

        return {
            config: { //传入组件数据

            }
        }


    },
    mounted() {

    },
    components: {
        IndexData1, IndexData2, IndexData3, IndexData4, IndexData5, IndexData6, IndexData7, IndexData8, IndexData9
    }

}
</script>
<style scoped>.box1 {
    width: 610px;
    height: 340px;
}

.box {
    display: flex;
    justify-content: space-between;
    width: 98%;
    margin: auto;

}</style>