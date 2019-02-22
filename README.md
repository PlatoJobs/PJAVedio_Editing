

#### 当视频直播可大致分为：
1.  视频录制端：一般是电脑上的音视频输入设备或者手机端的摄像头或者麦克风，目前以移动端的手机视频为主。
2.  视频播放端：可以是电脑上的播放器，手机端的native播放器，还有就是h5的video标签等，目前还是已手机端的native播放器为主。
3.  视频服务器端：一般是一台nginx服务器，用来接受视频录制端提供的视频源，同时提供给视频播放端流服务。

#### 下面将利用ios上的摄像头，进行音视频的数据采集，主要分为以下几个步骤：

1. 音视频的采集，ios中，利用AVCaptureSession和AVCaptureDevice可以采集到原始的音视频数据流。
2. 对视频进行H264编码，对音频进行AAC编码，在ios中分别有已经封装好的编码库来实现对音视频的编码。
3. 对编码后的音、视频数据进行组装封包；
4. 建立RTMP连接并上推到服务端。


>视频编码：所谓视频编码就是指通过特定的压缩技术，将某个视频格式的文件转换成另一种视频格式文件的方式，我们使用的iphone录制的视频，必须要经过编码，上传，解码，才能真正的在用户端的播放器里播放。
***iOS 音视频采集与编码***：
软编码：使用CPU进行编码 硬编码：使用非CPU进行编码，如显卡GPU、专用的DSP、FPGA、ASIC芯片等；
软编码：实现直接、简单，参数调整方便，升级易，但CPU负载重，性能较硬编码低，低码率下质量通常比硬编码要好一点。 
硬编码：性能高，低码率下通常质量低于软编码器，但部分产品在GPU硬件平台移植了优秀的软编码算法（如X264）的，质量基本等同于软编码。

>编解码标准：视频流传输中最为重要的编解码标准有国际电联的H.261、H.263、H.264，其中HLS协议支持H.264格式的编码。具体请移步至[iOS 音视频采集与编码](https://www.jianshu.com/p/11bb9f2a9233)
>音频编码：同视频编码类似，将原始的音频流按照一定的标准进行编码，上传，解码，同时在播放器里播放，当然音频也有许多编码标准，例如PCM编码，WMA编码，AAC编码等等，这里我们HLS协议支持的音频编码方式是AAC编码。

>：由于编码库大多使用c语言编写，需要自己使用时编译，对于ios，可以使用已经编译好的编码库。
>[x264编码](https://github.com/kewlbear/x264-ios)
>[faac编码](https://github.com/fflydev/faac-ios-build)
>[ffmpeg编码](https://github.com/kewlbear/FFmpeg-iOS-build-script)


简所谓推流，就是将我们已经编码好的音视频数据发往视频流服务器中，一般常用的是使用rtmp推流，可以使用第三方库`librtmp-iOS`进行推流，`librtmp`封装了一些核心的api供使用者调用，如果觉得麻烦，可以使用现成的ios视频推流sdk，也是基于`rtmp`的，[戳这里](https://github.com/runner365/LiveVideoCoreSDK)






