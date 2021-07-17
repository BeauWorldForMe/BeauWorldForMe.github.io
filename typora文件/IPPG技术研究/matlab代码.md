```matlab
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
axes(handles.axes1);
global vid;
vid.FramesPerTrigger = 300;
vidRes = vid.VideoResolution;
nBands = vid.NumberOfBands;
hImage = image( zeros(vidRes(2), vidRes(1), nBands) );
preview(vid,hImage);
```

```matlab
function pushbutton2_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
axes(handles.axes1);
global vid;
vid.FramesPerTrigger = 300;
start(vid);
pause(11)
% stop(vid);
stoppreview(vid);

diskLogger = VideoWriter('E:\课程缓存\动态数据处理\大作业\Classify.mp4', 'MPEG-4');
diskLogger.Quality = 100;
open(diskLogger);
data = getdata(vid, vid.FramesAvailable);
numFrames = size(data, 4);
for ii = 1:numFrames
    writeVideo(diskLogger, data(:,:,:,ii));
end
close(diskLogger);
```

```matlab
videoObj = VideoReader('Classify.mp4'); %读取视频
nframes = get(videoObj,'NumberOfFrames');
n=nframes;
for t = 1:n
    currentFrame = read(videoObj,t);
    image_name=strcat('E:\课程缓存\动态数据处理\大作业\摄像头所得\image_',num2str(t));
    image_name=strcat(image_name,'.jpg');
    imwrite(currentFrame,image_name,'jpg');      %写图片
end
```

