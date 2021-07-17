# 流程提纲

+ 点击**按钮1**调取摄像头（相当于预览窗口出现）

+ 点击**按钮2**摄像头录制一段10s的人脸视频，录制完成自动关闭摄像头并保存视频文件

+ **后面几个应该后台的流程，先用按钮来实现。**

  + 点击**按钮3**会把视频文件按帧提取，保留所有帧的图片到文件夹（按**image_1234**的顺序）

  + 点击**按钮4**通过第一帧来找到额头部位的坐标，得到一个坐标框

  + 点击**按钮5**对所有帧图像进行循环，把框里的每个点，用周围p*p大小的矩阵均值代替（绿色通道），存到数组里。画出波形并显示（IPPG信号）

    ```matlab
     bxjz2(1,1,t)=mean(mean(I2(round(conc_bboxes(1)-p/2):round(conc_bboxes(1)+p/2),round(conc_bboxes(2)-p/2):round(conc_bboxes(2)+p/2),2))); //这是matlab的代码
    ```

  + 点击**按钮6**对所有帧的整张图以q为步长进行遍历，还是让每个点的值等于周围p*p大小的矩阵均值（绿色通道），并把这些值以图像形式显示出来（人脸地形图）

    ```matlab
    c_r(((i-p/2-1)/q+1),((j-p/2-1)/q+1),t)=mean(mean(I2(i-p/2:i+p/2,j-p/2:j+p/2,2)));
    ```

    





```java
 @Override
    public void onDestroyView() {
        super.onDestroyView();
        if (mCameraSession != null) {
            mCameraSession.getDevice().close();
            mCameraSession.close();
        }
    }

    private void findview(View v) {
        mTextureView = (TextureView) v.findViewById(R.id.tv_textview);
        mButton = (Button) v.findViewById(R.id.btn_takepic);
        mThumbnail = (ImageView) v.findViewById(R.id.iv_Thumbnail);
        mThumbnail.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(getActivity(), "别戳了，那个页面还没写", Toast.LENGTH_SHORT).show();
            }
        });
    }

    /**
     * 播放系统的拍照的声音
     */
    public void shootSound() {
        ringtone.stop();
        ringtone.play();
    }

    private class ImageSaver implements Runnable {
        Image reader;

        public ImageSaver(Image reader) {
            this.reader = reader;
        }

        @Override
        public void run() {
            Log.d(TAG, "正在保存图片");
            File dir = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DCIM).getAbsoluteFile();
            if (!dir.exists()) {
                dir.mkdirs();
            }
            File file = new File(dir, System.currentTimeMillis() + ".jpg");
            FileOutputStream outputStream = null;
            try {
                outputStream = new FileOutputStream(file);
                ByteBuffer buffer = reader.getPlanes()[0].getBuffer();
                byte[] buff = new byte[buffer.remaining()];
                buffer.get(buff);
                BitmapFactory.Options ontain = new BitmapFactory.Options();
                ontain.inSampleSize = 50;
                Bitmap bm = BitmapFactory.decodeByteArray(buff, 0, buff.length, ontain);
                Message.obtain(mUIHandler, SETIMAGE, bm).sendToTarget();
                outputStream.write(buff);
                Log.d(TAG, "保存图片完成");
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                if (reader != null) {
                    reader.close();
                }
                if (outputStream != null) {
                    try {
                        outputStream.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }
        }
    }

    private class InnerCallBack implements Handler.Callback {
        @Override
        public boolean handleMessage(Message message) {
            switch (message.what) {
                case SETIMAGE:
                    Bitmap bm = (Bitmap) message.obj;
                    mThumbnail.setImageBitmap(bm);
                    break;
            }
            return false;
        }
    }
}
```

