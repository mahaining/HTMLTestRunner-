带图表分析的接口测试，有需要的可以直接拿去



添加代码：

    ECHARTS_SCRIPT = """
        <script type="text/javascript">
        var myChartline = echarts.init(document.getElementById('chartline'));
        var optionline = {
                tooltip: {
                trigger: 'axis',
                axisPointer: {
                    type: 'cross',
                    crossStyle: {
                        color: '#999'
                    }
                }
            },
            toolbox: {
                feature: {
                    dataView: {show: true, readOnly: false},
                    magicType: {show: true, type: ['line', 'bar']},
                    restore: {show: true},
                    saveAsImage: {show: true}
                }
            },
            legend: {
                data:['错误','成功','失败']
            },
            xAxis: [
                {
                    type: 'category',
                    data: [' 第一次','第二次','第三次','第四次','第五次','第六次','第七次','第八次','第九次','第十次'],
                    axisPointer: {
                        type: 'shadow'
                    }
                }
            ],
            yAxis: [
                {
                    type: 'value',
                    name: '百分比',
                    min: 0,
                    max: 100,
                    interval: 20,
                    axisLabel: {
                        formatter: '{value} %%'
                    }
                },
                {
                    type: 'value',
                    name: '成功率',
                    min: 0,
                    max: 10,
                    interval: 2,
                    axisLabel: {
                        formatter: '{value} %%'
                    }
                }
                
            ],
            series: [
                {
                    name:'成功',
                    type:'bar',
                    data:[%(Pass)s]
                //data:[2.0, 4.9, 7.0, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20.0, 6.4, 3.3]
                },
                {
                    name:'失败',
                    type:'bar',
                    data:[%(fail)s]
                },
                {
                    name:'错误',
                    type:'line',
                    yAxisIndex: 1,
                    data:[%(error)s]
                    //data:[2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2]
                }
            ]
        };
        myChartline.setOption(optionline);
        console.log(%(fail)s,%(Pass)s,%(error)s)
            // 基于准备好的dom，初始化echarts实例
            var myChart = echarts.init(document.getElementById('chart'));

            // 指定图表的配置项和数据
            var option = {
                title : {
                    text: '测试执行情况',
                    x:'center'
                },
                tooltip : {
                    trigger: 'item',
                    formatter: "{a} <br/>{b} : {c} ({d}%%)"
                },
                legend: {
                    orient: 'vertical',
                    left: 'left',
                    data: ['通过','失败','错误']
                },
                series : [
                    {
                        name: '测试执行情况',
                        type: 'pie',
                        radius : '60%%',
                        center: ['50%%', '60%%'],
                        data:[
                            {value:%(Pass)s, name:'通过'},
                            {value:%(fail)s, name:'失败'},
                            {value:%(error)s, name:'错误'}
                        ],
                        itemStyle: {
                            emphasis: {
                                shadowBlur: 10,
                                shadowOffsetX: 0,
                                shadowColor: 'rgba(0, 0, 0, 0.5)'
                            }
                        }
                    }
                ]
            };

            // 使用刚指定的配置项和数据显示图表。
            myChart.setOption(option);
        </script>
        
