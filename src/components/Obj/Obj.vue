<template>
    <div id="page-content"></div>
</template>

<script>
    import { options } from '../../config/option'
    import { pid } from '../../config/project-pid'
    import { pose } from '../../config/pose'
    export default {
        name: "Obj",
        data () {
            return {
                pointList: [], // 收集点,
                sandbox: '', // 初始化沙盒为空,
                marker: '' // 初始化一个projectMarker
            }
        },
        methods: {
            handler (event) {
                let pt =  this.sandbox.pickOnProjects(event)
                console.log('------', pt)
                if (!pt) {
                    return
                }
                console.log('onclick point coordinate', pt)
                this.pointList.push(pt)
                this.$nextTick(() => {
                    let res = this.pointList.map(item => [item.lng, item.lat, item.alt])
                    console.log(JSON.stringify(res))
                })
                // alert(`longitude: ${pt.lng}(deg), latitude: ${pt.lat}(deg), altitude ${pt.alt}(m)`)

                let tag = new altizure.TagMarker({
                    // img urlR
                    imgUrl: '/assets/img/tag/normal/tagDemo.png',
                    // icon position
                    position: {
                        "lng": pt.lng,
                        "lat": pt.lat,
                        "alt": pt.alt
                    },
                    // scene
                    sandbox:  this.sandbox,
                    scale: 0.5 // icon size
                })

                let tt = new altizure.TextTagMarker({
                    // text string
                    //text: `(${pt.lng.toPrecision(9)}, ${pt.lat.toPrecision(9)}, ${pt.alt.toPrecision(7)})`,
                    text: ' ',
                    // text style
                    textStyle: {
                        fillStyle: 'rgb(255, 255, 255)',
                        font: 'normal 500 24px Arial',
                        outlineWidth: 2,
                        outlineStyle: 'rgb(0, 0, 0)'
                    },

                    // icon position
                    position: {
                        "lng": pt.lng,
                        "lat": pt.lat,
                        "alt": pt.alt
                    },
                    // scene
                    sandbox:  this.sandbox,
                    scale: 1 // icon size
                })

            }, // 收集点时的事件回调函数
            initProject () {
                // 生成沙盒
                this.sandbox = new altizure.Sandbox('page-content', options)
                // 将模型添加到沙盒中
                this.sandbox.add('AltizureProjectMarker', {pid})
                // 保存返回的AltizureProjectMarker实例
                return this.sandbox.add('AltizureProjectMarker', {
                    // 这是一个异步函数, 再加载完projectmarker之后返回一个promise对象
                    pid,
                    pose
                })
            }, // 初始化项目
            addTextTag (text, position) {
                let objTag = new altizure.TextTagMarker({
                    text,
                    textStyle: {
                        fillStyle: 'rgb(255, 255, 255)',
                        font: '500 36px Arial',
                        margin:5,
                        outlineWidth: 0.1,
                        outlineStyle: 'rgb(0, 0, 0)'
                    },
                    position,
                    pivot: {
                        y: 0,
                        x: 0.5,
                    },
                    isSprite : true,
                    pivotx : 0.5,
                    pivoty : 0,
                    pinLength : 10,
                    scale: 0.5, // icon size
                    sandbox:  this.sandbox,
                })
            }, // obj文字标签
            addTextTags () {
                // 文字标签
                let textTagList = [
                    {
                        text: '观测点1',
                        position: {
                            "lng": 114.26660928555647,
                            "lat": 22.337686476540696,
                            "alt": 32.650745890428375
                        }
                    },
                    {
                        text: '观测点2',
                        position: {
                            "lng": 114.26602286177834,
                            "lat": 22.33733334117565,
                            "alt": 32.650745890428375
                        }
                    },
                    {
                        text: '观测点3',
                        position: {
                            "lng": 114.26624962948686,
                            "lat": 22.336151356503848,
                            "alt": 40.1698350852244
                        }
                    }
                ]
                textTagList.forEach((item, index) => {
                    let name = 'textTag' + index
                    let {text, position} =item
                    name = new altizure.TextTagMarker({
                        // text string
                        text,
                        // text style
                        textStyle: {
                            fillStyle: 'rgb(255, 255, 255)',
                            font: '500 36px Arial',
                            margin: 10,
                            outlineWidth: 0.1,
                            outlineStyle: 'rgb(0, 0, 0)',
                        },
                        pivot: {
                            y: -0.8,
                            x: 0.5,
                        },
                        isSprite : true,
                        pivotx : 0.5,
                        pivoty : -0.8,
                        pinLength : 25,
                        // icon position
                        position,
                        // scene
                        sandbox:  this.sandbox,
                        scale: 0.5 // icon size
                    })
                })
            }, // 增加若干个文字标签
            addObj () {
                // obj模型
                let obj = new altizure.OBJMarker({
                    position: {
                        lng: 114.26621311927057,
                        lat: 22.33692591410213,
                        alt: 39.11879849220491
                    },
                    sandbox:  this.sandbox,
                    name: 'arbor',
                    shape: 'CUSTOMIZE',
                    objUrl: '/assets/object/arbor/arbor.obj',
                    mtlUrl: '/assets/object/arbor/arbor.mtl',
                    upDir: {x: 0,y: 1,z: 0},
                    "scale": 5
                })
            }, // 增加模型
            addPoly () {
                // 多边形
                let pts1 = [
                    [114.26612219943183, 22.336301330418983, 40.05124295152777],
                    [114.26609591181227, 22.336573448255617,39.57224353075798],
                    [114.2662914291679, 22.33655793317073, 38.76812322809311],
                    [114.26630746711534, 22.336294587113613, 39.45521357816167],
                    [114.26612219943183, 22.336301330418983, 40.05124295152777],
                ].map(function(lnglatalt)  {
                    return new altizure.LngLatAlt(lnglatalt[0], lnglatalt[1], lnglatalt[2])
                })
                let pl1 = new altizure.PolyLineMarker({
                    name: 'pl1',
                    sandbox:  this.sandbox,
                    points: pts1,
                    color: 0xb73026, // line color
                    fenceHeight: 10, // line height (for visualization)
                })
                pl1.style = {animation: 'vertical'}
            }, // 增加多边形,
            addPolyLine () {
                // 添加箭头
                let pts3 = [
                    [114.2665033161682, 22.33624869996219,32.649188963586326],
                    [114.26651585022066, 22.33639714302435, 31.333683931086266],
                    [114.26648780059543, 22.33660497135859, 32.284286371388],
                    [114.26648588585577, 22.3367875471929, 32.258352147920114],
                    [114.26650812455503, 22.33694105189148, 32.237116169557886],
                    [114.26654148392738, 22.337107307736364, 32.48487471499218],
                    [114.26656126769811, 22.33729510415698, 31.482357040436224],
                    [114.26658009941872, 22.337446376997622, 31.04037843878511],
                    [114.26661040075295, 22.3376286039461, 30.45113090041977],
                    [114.26667906689588, 22.33776782041247, 30.087527565628367]
                ]
                    .map(function(lnglatalt) {
                        return new altizure.LngLatAlt(lnglatalt[0], lnglatalt[1], lnglatalt[2])
                    })
                let pl3 = new altizure.PolyLineMarker({
                    name: 'pl3',
                    sandbox:  this.sandbox,
                    points: pts3,
                    color: 0x26b74f,
                    fenceHeight: 10
                })
                pl3.style = {
                    texture: 'arrow',
                    mapping: 'repeat'
                }
                pl3.speed = 1.0
            }  // 增加带箭头的线
        },
        mounted() {
            this.initProject().then(m => {
                this.marker = m // 得到marker
                setTimeout(() => {
                    // 设置事件, 用于收集描的点
                    document.addEventListener('click', this.handler)
                    document.addEventListener('touchstart', this.handler)

                    this.addTextTag('obj标签', {
                        "lng": 114.26610742184087,
                        "lat": 22.336769578829614,
                        "alt": 39.5143430135647
                    })
                    this.addObj()
                    this.addTextTag()
                    this.addTextTags()
                    this.addPoly()
                    this.addTextTag('矩形', {
                        "lng": 114.26614881038299,
                        "lat": 22.336405238451412,
                        "alt": 39.33534860982993
                    })
                    this.addPolyLine()
                }, 200)
                })

        }
    }
</script>

<style scoped>

</style>
