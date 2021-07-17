```java
   public static final int SHOW_RESPONSE = 0;
    private Button button_sendRequest;
    private TextView textView_response;
    //新建Handler的对象，在这里接收Message，然后更新TextView控件的内容
    private Handler handler = new Handler() {
        @Override
        public void handleMessage(Message msg) {
            super.handleMessage(msg);
            switch (msg.what) {
                case SHOW_RESPONSE:
                    String response = (String) msg.obj;
                    textView_response.setText(response);
                    break;
                default:
                    break;
            }
        }
    };


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);
//        request("https://icloud.tianzhongyimai.com:10082");
//        TextView textView2 = findViewById(R.id.getData);
//        textView2.setText(result2);
        textView_response = (TextView)findViewById(R.id.TextView1);
        button_sendRequest = (Button)findViewById(R.id.button1);
        button_sendRequest.setOnClickListener(new View.OnClickListener() {
            //点击按钮时，执行sendRequestWithHttpClient()方法里面的线程
            @Override
            public void onClick(View v) {
                // TODO Auto-generated method stub
                sendRequestWithHttpClient();
            }
        });
    }
    private void sendRequestWithHttpClient() {
        //方法：发送网络请求，获取网页的数据。在里面开启线程
        new Thread(new Runnable() {
            @Override
            public void run() {
                //用HttpClient发送请求，分为五步
                //第一步：创建HttpClient对象
                HttpClient httpCient = new DefaultHttpClient();
                //第二步：创建代表请求的对象,参数是访问的服务器地址
                HttpGet httpGet = new HttpGet("https://icloud.tianzhongyimai.com/patientInformation");

                //放入请求头的内容，以键值对的形式
                httpGet.addHeader("Content-type","application/json");
                //获取请求头，并用Header数组接收
                Header[] reqHeaders = httpGet.getAllHeaders();
                //遍历Header数组，并打印出来
                for (int i = 0; i < reqHeaders.length; i++) {
                    String name = reqHeaders[i].getName();
                    String value = reqHeaders[i].getValue();
                    Log.d("内容", "http request:name--->" + name + "value--->" + value);
                }

                try {
                    //第三步：执行请求，获取服务器发还的相应对象
                    HttpResponse httpResponse = httpCient.execute(httpGet);
                    //获取响应头，并用Header数组接收
                    Header [] responseHeaders = httpResponse.getAllHeaders();
                    //遍历Header数组，并打印出来
                    for (int i = 0; i < responseHeaders.length; i++) {
                        String name = responseHeaders[i].getName();
                        String value = responseHeaders[i].getValue();
                        Log.d("内容", "http response:name--->" + name + "value--->" + value);
                    }

                    //第四步：检查响应的状态是否正常：检查状态码的值是200表示正常
                    if (httpResponse.getStatusLine().getStatusCode() == 200) {
                        //第五步：从响应对象当中取出数据，放到entity当中
                        HttpEntity entity = httpResponse.getEntity();
                        String response = EntityUtils.toString(entity,"utf-8");//将entity当中的数据转换为字符串
                        //在子线程中将Message对象发出去
                        Message message = new Message();
                        message.what = SHOW_RESPONSE;
                        message.obj = response.toString();
                        handler.sendMessage(message);
                    }} catch (Exception e) {
                    e.printStackTrace();
                }

            }

        }).start();
    }
}
```