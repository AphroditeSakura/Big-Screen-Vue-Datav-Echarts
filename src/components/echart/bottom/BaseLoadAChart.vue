<template>
    <div id="load-map" class="load-map"></div>
</template>

<script>
    import echartMixins from "@/utils/resizeMixins";
    export default
    {
        data()
        {
        return {chart: null}
        },
        mixins: [echartMixins],
        mounted()
        {
            this.draw();
        },
        methods:{
            refresh(data){
               let option= this.chart.getOption()
               let list_0= new Array()
               for(let index=0;index<data.length;index++){
                   list_0= data[index]
                   option.dataset.unshift(list_0)
                }
                this.chart.setOption(option);
            },
            draw()
            {
                this.chart = this.$echarts.init(document.getElementById('load-map'),'dark');
                let load_option =
                    {
                    legend: {},
                    tooltip: {
                        trigger: 'axis',
                        showContent: true
                    },
                    dataset: {
                        source: [
                            ['month',  '2020', '2021', '2022'],
                            ['1', 70.1, 53.4, 85.1],
                            ['2', 51.1,  68.7, 40.1],
                            ['3', 40.1, 62.2, 68.7],
                            ['4', 56.5, 82.1, 85.1],
                            ['5', 51.1, 68.7, 40.1],
                            ['6', 40.1, 62.2,  68.7],
                            ['7', 56.5, 53.4, 85.1],
                            ['8', 51.1, 68.7, 40.1],
                            ['9', 40.1, 32.5, 68.7],
                            ['10', 56.5,  53.4, 85.1],
                            ['11', 51.1,  68.7, 40.1],
                            ['12', 40.1, 62.2,  68.7]
                        ]
                    },
                    xAxis: {
                        type: 'category'
                    },
                        name: '月份'
                        , type: 'value',
                        axisLabel: {
                            formatter: '{value} 月'},
                    yAxis: {
                        name: '冷量'
                        , type: 'value',
                        axisLabel: {
                            formatter: '{value} RT'
                        }
                    },
                    series:
                        [
                            {
                                name:"2020年冷量",
                                type: 'line',
                            },
                            {
                                name:"2021年冷量",
                                type: 'line',
                            },
                            {
                                name:"2022年冷量",
                                type: 'line',
                            }]
                }
                this.chart.setOption(load_option);
            }
        }
    }


</script>

<style scoped>
.load-map{
   padding-top: 10px;
    width: 100%;
    height:100%;
    overflow: hidden;
    margin-bottom: 0px;
}
</style>