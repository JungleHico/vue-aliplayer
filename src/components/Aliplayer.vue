<template>
  <div class='prism-player' :id='playerId'>
      <slot></slot>
  </div>
</template>

<script>

const aliplayerSdkPath = '//g.alicdn.com/de/prismplayer/2.8.2/aliplayer-min.js'

export default {
    name: 'Aliplayer',
    props: {
        source: {
            type: String,
            default: ''
        },
        vid: {
            type: String,
            default: ''
        },
        playauth: {
            type: String,
            default: ''
        },
        width: {
            type: String,
            default: '100%'
        },
        height: {
            type: String,
            default: '320px'
        },
        videoWidth: {
            type: String,
            default: '100%'
        },
        videoHeight: {
            type: String,
            default: '100%'
        },
        preload: {
            type: Boolean,
            default: false
        },
        cover: {
            type: String,
            default: ''
        },
        isLive: {
            type: Boolean,
            default: false
        },
        autoplay: {
            type: Boolean,
            default: false
        },
        rePlay: {
            type: Boolean,
            default: false
        },
        useH5Prism: {
            type: Boolean,
            default: false
        },
        useFlashPrism: {
            type: Boolean,
            default: false
        },
        playsinline: {
            type: Boolean,
            default: false
        },
        showBuffer: {
            type: Boolean,
            default: true
        },
        skinRes: {
            type: String,
            default: ''
        },
        skinLayout: {
            type: Array
        },
        controlBarVisibility: {
            type: String,
            default: 'hover'
        },
        showBarTime: {
            type: String,
            default: ''
        },
        extraInfo: {
            type: String,
            default: ''
        },
        enableSystemMenu: {
            type: Boolean,
            default: false
        },
        format: {
            type: String,
            default: ''
        },
        mediaType: {
            type: String,
            default: 'video'
        },
        qualitySort: {
            type: String,
            default: 'asc'
        },
        definition: {
            type: String,
            default: ''
        },
        defaultDefinition: {
            type: String,
            default: ''
        },
        x5_type: {
            type: String,
            default: 'h5'
        },
        x5_fullscreen: {
            type: Boolean,
            default: false
        },
        x5_video_position: {
            type: String,
            default: 'center'
        },
        x5_orientation: {
            type: String,
            default: 'portrait'
        },
        // TODO 待测
        x5LandscapeAsFullScreen: {
            type: Boolean,
            default: true
        },
        autoPlayDelay: {
            type: Number,
            default: 0
        },
        autoPlayDelayDisplayText: {
            type: String,
            default: '正在转码，请稍后......'
        },
        language: {
            type: String,
            default: 'zh-cn'
        },
        languageTexts: {
            type: Object,
            default() {
                return {}
            }
        },
        snapshot: {
            type: Boolean,
            default: false
        },
        snapshotWatermark: {
            type: Object,
            default() {
                return {}
            }
        },
        useHlsPluginForSafari: {
            type: Boolean,
            default: false
        },
        enableStashBufferForFlv: {
            type: Boolean,
            default: false
        },
        stashInitialSizeForFlv: {
            type: Number,
            default: 10
        },
        loadDataTimeout: {
            type: Number,
            default: 20
        },
        waitingTimeout: {
            type: Number,
            default: 60
        },
        liveStartTime: {
            type: String,
            default: ''
        },
        liveOverTime: {
            type: String,
            default: ''
        },
        liveTimeShiftUrl: {
            type: String,
            default: ''
        },
        liveShiftSource: {
            type: String,
            default: ''
        },
        recreatePlayer: {
            type: Function,
            default: () => {
            }
        },
        diagnosisButtonVisible: {
            type: Boolean,
            default: true
        },
        disableSeek: {
            type: Boolean,
            default: false
        },
        encryptType: {
            type: Number,
            default: 0
        },
        progressMarkers: {
            type: Array,
            default: () => []
        },
        vodRetry: {
            type: Number,
            default: 3
        },
        liveRetry: {
            type: Number,
            default: 5
        },
    },
    data() {
        return {
            playerId: 'aliplayer_' + Math.random() * 100000000000000000,
            instance: null
        }
    },
    created() {
        if (window.Aliplayer) {
            this.initAliplayer()
        } else {
            this.insertScriptTag()
        }
    },
    methods: {
    // 插入播放器脚本
        insertScriptTag() {
            let playerScriptTag = document.getElementById('playerScriptTag')
            if (playerScriptTag === null) {
                playerScriptTag = document.createElement('script')
                playerScriptTag.src = aliplayerSdkPath
                playerScriptTag.id = 'playerScriptTag'
                let head = document.getElementsByTagName('head')[0]
                head.appendChild(playerScriptTag)
            }
            playerScriptTag.addEventListener('load', () => {
                this.initAliplayer()
            })
        },
        // 初始化播放器
        initAliplayer() {
            if (this.instance === null) {
                this.$nextTick(() => {
                    this.instance = window.Aliplayer({
                        id: this.playerId,
                        source: this.source,
                        vid: this.vid,
                        playauth: this.playauth,
                        width: this.width,
                        height: this.height,
                        videoWidth: this.videoWidth,
                        videoHeight: this.videoHeight,
                        preload: this.preload,
                        cover: this.cover,
                        isLive: this.isLive,
                        autoplay: this.autoplay,
                        rePlay: this.rePlay,
                        useH5Prism: this.useH5Prism,
                        useFlashPrism: this.useFlashPrism,
                        playsinline: this.playsinline,
                        showBuffer: this.showBuffer,
                        skinRes: this.skinRes,
                        skinLayout: this.skinLayout,
                        controlBarVisibility: this.controlBarVisibility,
                        showBarTime: this.showBarTime,
                        extraInfo: this.extraInfo,
                        enableSystemMenu: this.enableSystemMenu,
                        format: this.format,
                        mediaType: this.mediaType,
                        qualitySort: this.qualitySort,
                        definition: this.definition,
                        defaultDefinition: this.defaultDefinition,
                        x5_type: this.x5_type,
                        x5_fullscreen: this.x5_fullscreen,
                        x5_video_position: this.x5_video_position,
                        x5_orientation: this.x5_orientation,
                        x5LandscapeAsFullScreen: this.x5LandscapeAsFullScreen,
                        autoPlayDelay: this.autoPlayDelay,
                        autoPlayDelayDisplayText: this.autoPlayDelayDisplayText,
                        language: this.language,
                        languageTexts: this.languageTexts,
                        snapshot: this.snapshot,
                        snapshotWatermark: this.snapshotWatermark,
                        useHlsPluginForSafari: this.useHlsPluginForSafari,
                        enableStashBufferForFlv: this.enableStashBufferForFlv,
                        stashInitialSizeForFlv: this.stashInitialSizeForFlv,
                        loadDataTimeout: this.loadDataTimeout,
                        waitingTimeout: this.waitingTimeout,
                        liveStartTime: this.liveStartTime,
                        liveOverTime: this.liveOverTime,
                        liveTimeShiftUrl: this.liveTimeShiftUrl,
                        liveShiftSource: this.liveShiftSource,
                        recreatePlayer: this.recreatePlayer,
                        diagnosisButtonVisible: this.diagnosisButtonVisible,
                        disableSeek: this.disableSeek,
                        encryptType: this.encryptType,
                        progressMarkers: this.progressMarkers,
                        vodRetry: this.vodRetry,
                        liveRetry: this.liveRetry
                    })

                    // 播放器事件监听
                    this.instance.on('ready', () => {
                        this.$emit('ready', this.instance)
                    })
                    this.instance.on('play', () => {
                        this.$emit('play', this.instance)
                    })
                    this.instance.on('pause', () => {
                        this.$emit('pause', this.instance)
                    })
                    this.instance.on('canplay', () => {
                        this.$emit('canplay', this.instance)
                    })
                    this.instance.on('playing', () => {
                        this.$emit('playing', this.instance)
                    })
                    this.instance.on('ended', () => {
                        this.$emit('ended', this.instance)
                    })
                    this.instance.on('liveStreamStop', () => {
                        this.$emit('liveStreamStop', this.instance)
                    })
                    this.instance.on('onM3u8Retry', () => {
                        this.$emit('onM3u8Retry', this.instance)
                    })
                    this.instance.on('hideBar', () => {
                        this.$emit('hideBar', this.instance)
                    })
                    this.instance.on('showBar', () => {
                        this.$emit('showBar', this.instance)
                    })
                    this.instance.on('waiting', () => {
                        this.$emit('waiting', this.instance)
                    })
                    this.instance.on('timeupdate', () => {
                        this.$emit('timeupdate', this.instance)
                    })
                    this.instance.on('snapshoted', () => {
                        this.$emit('snapshoted', this.instance)
                    })
                    this.instance.on('requestFullScreen', () => {
                        this.$emit('requestFullScreen', this.instance)
                    })
                    this.instance.on('cancelFullScreen', () => {
                        this.$emit('cancelFullScreen', this.instance)
                    })
                    this.instance.on('error', () => {
                        this.$emit('error', this.instance)
                    })
                    this.instance.on('startSeek', () => {
                        this.$emit('startSeek', this.instance)
                    })
                    this.instance.on('completeSeek', () => {
                        this.$emit('completeSeek', this.instance)
                    })
                })
            }
        },
        // 播放器接口
        play() {
            this.instance.play()
        },
        pause() {
            this.instance.pause()
        },
        replay() {
            this.instance.replay()
        },
        seek(time) {
            this.instance.seek(time)
        },
        getCurrentTime() {
            return this.instance.getCurrentTime()
        },
        getDuration() {
            return this.instance.getDuration()
        },
        getVolume() {
            return this.instance.getVolume()
        },
        setVolume(vol) {
            this.instance.setVolume(vol)
        },
        loadByUrl(url, time) {
            this.instance.loadByUrl(url, time)
        },
        replayByVidAndPlayAuth(vid, playauth) {
            this.instance.replayByVidAndPlayAuth(vid, playauth)
        },
        replayByVidAndAuthInfo(vid, accId, accSecret, stsToken, authInfo, domainRegion) {
            this.instance.replayByVidAndAuthInfo(vid, accId, accSecret, stsToken, authInfo, domainRegion)
        },
        setPlayerSize(w, h) {
            this.instance.setPlayerSize(w, h)
        },
        setSpeed(speed) {
            this.instance.setSpeed(speed)
        },
        setSanpshotProperties(width, height, rate) {
            this.instance.setSanpshotProperties(width, height, rate)
        },
        requestFullScreen() {
            this.instance.fullscreenService.requestFullScreen()
        },
        cancelFullScreen() {
            this.instance.fullscreenService.cancelFullScreen()
        },
        getIsFullScreen() {
            return this.instance.fullscreenService.getIsFullScreen()
        },
        getStatus() {
            return this.instance.getStatus()
        },
        setLiveTimeRange(startTime, endTime) {
            this.instance.setLiveTimeRange(startTime, endTime)
        },
        setRotate(deg) {
            this.instance.setRotate(deg)
        },
        getRotate() {
            return this.instance.getRotate()
        },
        setImage(image) {
            this.instance.setImage(image)
        },
        dispose() {
            this.instance.dispose()
        },
        setCover(cover) {
            this.instance.setCover(cover)
        },
        setProgressMarkers(markers) {
            this.instance.setProgressMarkers(markers)
        },
        setPreviewTime(time) {
            this.instance.setPreviewTime(time)
        },
        getPreviewTime() {
            return this.instance.getPreviewTime()
        },
        isPreview() {
            return this.instance.isPreview()
        }
    }
}
</script>

<style scoped>
@import url(//g.alicdn.com/de/prismplayer/2.8.2/skins/default/aliplayer-min.css);

.prism-player {
    overflow: hidden;
}

</style>
