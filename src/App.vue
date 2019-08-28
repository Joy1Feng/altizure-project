<template>
    <div id="app">
        <div id="page-content"></div>
    </div>
</template>

<script>
import HelloWolrd from './components/HelloWorld'
export default {
    name: 'app',
    components: {
        HelloWolrd
    },
    data () {
        return {
            options: {
                altizureApi:{
                    key: '7MkQf8UggsPaadvrlKALspJWZejZAJOLHn3cnIy'
                },
                camera: {
                    center: { alt: 319.02169601663104,
                        lat: 22.5364271949327,
                        lng: 113.93977612840078,
                        north: 56.82289356559219,
                        tilt: 56.19205822511624 },
                    flyToCenter: { alt: 319.02169601663104,
                        lat: 22.5364271949327,
                        lng: 113.93977612840078,
                        north: 56.82289356559219,
                        tilt: 56.19205822511624 }
                },
                renderItems: {
                    earth: true,
                    earthUseTexture: false,
                    featureInView: false,
                    orbitRing: false
                }
            }
        }
    },
    mounted() {
        let sandbox = new altizure.Sandbox('page-content', this.options)

        sandbox.add('AltizureProjectMarker', {pid: '5849104597b73e0b090c01e8'})

        let textTag = new altizure.TextTagMarker({
            // text string
            text: '深圳珠峰科技',
            // text style
            textStyle: {
                fillStyle: 'rgb(255, 255, 255)',
                font: '500 60px Arial',
                margin:5,
                outlineWidth: 0.1,
                outlineStyle: 'rgb(0, 0, 0)'
            },

            // icon position
            position: {
                "lng": 113.939190,
                "lat": 22.5369807,
                "alt": 33.31495
            },
            // scene
            sandbox: sandbox,
            scale: 0.5 // icon size
        })
    }
}
</script>

<style>
    * {
        margin: 0;
        padding: 0;
    }

    html, body {
        width: 100%;
        height: 100%;
    }

    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        width: 100%;
        height: 100%
    }

    #page-content {
        width: 100%;
        height: 100%;
    }
</style>
