<template>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 198.43 283.46"
        id="ueg-card">
        <rect class="a" width="198.43" height="283.46" />
        <rect class="b" x="51.02" width="147.4" height="283.46" />
        <image width="249" height="336" transform="translate(28 43) scale(0.26)" :xlink:href="_avatorDataUri" />
        <text class="c" transform="translate(19.77 159.64)">Name:</text>
        <text class="d" transform="translate(57.62 167.51)">{{ surname }}</text>
        <text class="e" transform="translate(57.89 182.57)">{{ givenname }}
        </text>
        <text class="c" transform="translate(10.03 213.66)">Position:</text>
        <text class="e" transform="translate(57.17 213.38)">{{ position }}
        </text>
        <rect class="i" x="12.21" y="257.12" width="174" height="13" rx="2.83" />
        <image width="680" height="50" transform="translate(20.5 257.8) scale(0.24)" :xlink:href="getBar" />
        <polygon points="17 263.83 20 265.67 20 262 17 263.83" />
        <text class="j" transform="translate(44.18 29.05) scale(1.25 0.9)">UNITED EARTH GOVERNMENT
        </text>
        <image width="357" height="272" transform="translate(12 18) scale(0.06)"
            xlink:href="data:image/png;base64,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" />
        <rect class="i" x="134.06" y="52" width="47" height="56" />
        <polygon points="157.4 60 162.06 56 152.73 56 157.4 60" />
        <image width="300" height="300" transform="translate(136.5 63) scale(0.14)" :xlink:href="getQR" />
        <text class="n" transform="translate(135.94 119.32)">{{ getDate }}
        </text>
    </svg>

</template>
<script>
import moment from 'moment'
import kjua from 'kjua'
import JsBarcode from 'jsbarcode'
import '../card.css'

function blob2DataURI(blob) {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(blob);
        reader.onload = () => resolve(reader.result);
        reader.onerror = error => reject(error);
    });

}

function svg2b64(svg) {
    let s = svg.outerHTML
    return `data:image/svg+xml;base64,${window.btoa(s)}`
}

export default {
    props: ['surname', 'givenname', 'position', 'avator'],
    data() {
        return {
            _avatorDataUri: './LiXuejian.png'
        }
    },
    computed: {
        codeContent() {
            return `${this.surname}<<<${this.givenname}`
        },
        getDate() {
            let now = moment().year(2044).format('DD MMM YYYY')
            return now.toString().toUpperCase()
        },
        getQR() {
            let qr = kjua({
                render: 'svg',
                ecLevel: 'L',
                fill: '#000',
                size: 300,
                ratio: null,
                rounded: 0,
                quiet: 2,
                mode: 'plain',
                text: this.codeContent
            })

            return svg2b64(qr)
        },
        getBar() {
            let svg = document.createElement('svg')
            JsBarcode(svg, this.codeContent, {
                height: 8,
                displayValue: false,
                margin: 3,
                marginLeft: 5
            })
            return svg2b64(svg)
        },
    },
    watch: {
        avator() {
            if (this.avator) {
                let b = new Blob([this.avator], { type: this.avator.type })
                blob2DataURI(b).then((v) => {
                    this._avatorDataUri = v
                })
            }
        },
    }
}
</script>

<style scoped>

</style>
