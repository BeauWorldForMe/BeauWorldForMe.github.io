接口

```java
/**
 * @Description: 接口定义API
 * @author: sjg
 * @Date: 2018/3/26 17:07
 */

public interface ProjectApi {
    /**
     * 医生端登录接口
     *
     * @return
     */
    @POST("auth/admin/login")
    Observable<BaseResult<DoctorInfo>> getAdminLogin(@Body RequestBody params);

    /**
     * 医生详情接口
     *
     * @return
     */
    @POST("api/doctor-info")
    Observable<BaseResult<DoctorDetail>> getDoctorInfo(@Header("Authorization") String token, @Body RequestBody params);

    /**
     * 病人端登录接口
     *
     * @return
     */
    @POST("auth/user/login")
    Observable<BaseResult<UserInfo>> getUserLogin(@Body RequestBody params);

    /**
     * 查询所有既往病例
     *
     * @return
     */
    @GET("api/anamnesis-question-bank")
    Observable<BaseResult<List<CaseHistoryNewBean>>> getAnamnesisAll(@Header("Authorization") String token, @Query("doctorId") int id);

    /**
     * 发送既往病例选择结果
     *
     * @return
     */
    @PUT("api/anamnesis")
    Observable<BaseResult<AddAnamnesisBean>> addAnamnesis(@Header("Authorization") String token, @Body RequestBody params);

    /**
     * 获取题目接口（三十六种体质）
     *
     * @return
     */
    @GET("api/selectConstitutionQuestion")
    Observable<BaseResult<List<CorporeityCheckNewBean>>> getTitleList(@Header("Authorization") String token, @Query("doctorId") String doctorId, @Query("questionType") int questionType, @Query("isAll") int isAll);

    /**
     * 发送答案-简易九种体质接口
     *
     * @return
     */
//    @POST("api/constitution-result")
    @POST("api/answer/up")
    Observable<BaseResult> getSimple(@Header("Authorization") String token, @Body RequestBody params);

    /**
     * 用户登录
     *
     * @return
     */
//    @GET("appLogin.do")
//    Observable<BaseResult<UserManyInfo>> userLogin(@Query("userName") String userName, @Query("passWord") String password);
    @POST("login")
    Observable<BaseResult<UserInfo>> userLogin(@Body RequestBody params);


    /**
     * 上传文件
     *
     * @param token
     * @param file
     * @return
     */
    @Multipart
    @POST("api/up/image")
    Observable<BaseResult> uploadFile(@Header("Authorization") String token, @Part List<MultipartBody.Part> file);

    /**
     * 查询题目类型
     *
     * @return
     */
    @GET("api/titleType/query")
    Observable<BaseResult<TitleType>> getTitleType(@Header("Authorization") String token);

    /**
     * 修改医生信息接口
     */
    @POST("api/modification/doctor-information")
    Observable<BaseResult> saveDoctorInformation(@Header("Authorization") String token, @Body RequestBody params);

    /**
     * 医生确认密码接口
     */
    @POST("api/doctor/confirmPwd")
    Observable<BaseResult> doctorConfirmPwd(@Header("Authorization") String token, @Body RequestBody params);

    /**
     * 获取病人检测结果
     *
     * @param caseHistoryNum
     * @return
     */
    @GET("api/answer/result")
    Observable<BaseResult<GetAnswerResultBean>> getDiagnosisResult(@Header("Authorization") String token, @Query("caseHistoryNum") String caseHistoryNum);


    /**
     * 获取分享检测结果 的地址
     *
     * @return
     */
    @GET("api/answer/share")
    Observable<BaseResult<GetAnswerShareUrlBean>> getAnswerShareUrl(@Header("Authorization") String token, @Query("caseHistoryNum") String caseHistoryNum);


    /**
     * 生成病历号
     *
     * @return
     */
    @GET("auth/getCaseHistoryNum")
    Observable<BaseResult> getCaseHistoryNum(@Query("doctorId") String doctorId);

    /**
     * 获取舌像结果接口
     *
     * @return
     */
    @GET("api/tongueImg/result")
    Observable<BaseResult> getSheXiangResult(@Header("Authorization") String token, @Query("caseHistoryNum") String caseHistoryNum);

    /**
     * 获取面相结果接口
     *
     * @return
     */
    @GET("api/faceImg/result")
    Observable<BaseResult> getFaceResult(@Header("Authorization") String token, @Query("caseHistoryNum") String caseHistoryNum);

    /**
     * 查询病例答题选项结果
     *
     * @return
     */
    @GET("api/getCaseHistoryAnswer")
    Observable<BaseResult> getCaseHistoryAnswer(@Header("Authorization") String token, @Query("caseHistoryNum") String caseHistoryNum);

    /**
     //     * 体质诊断答题发送接口（修改）
     //     *
     //     * @return
     //     */
//    @GET("api/getCaseHistoryAnswer")
//    Observable<BaseResult> getCaseHistoryAnswer(@Header("Authorization") String token, @Query("caseHistoryNum") String caseHistoryNum);


    /**
     * 查询所有病人接口、病人姓名查询接口
     */
    @POST("api/query/historyUsername")
    Observable<BaseResult> queryPatientInfo(@Header("Authorization") String token, @Body RequestBody params);


    /**
     * 根据姓名查询
     */
    @POST("api/query/historyUsername")
    Observable<BaseResult> queryPatientName(@Header("Authorization") String token, @Query("historyUsername") String historyUsername, @Body RequestBody params);

    /**
     * 查询医生留言接口
     */
    @GET("api/getCaseHistoryMessage")
    Observable<BaseResult> getCaseHistoryLeaveMessage(@Header("Authorization") String token, @Query("caseHistoryId") String caseHistoryNum);

    /**
     * 慢性病诊断结果问诊结果 查询接口
     */
    @GET("api/chronicDiseaseDiagnoseResult")
    Observable<BaseResult> getManXingBingResult(@Header("Authorization") String token, @Query("caseHistoryId") String caseHistoryNum);

}
```

```java
/**
 * @Description: SSL以及https工具
 * @author: wfx
 * @email: wfx19930411@163.com
 * @Date: 2018/3/26 13:57
 */

public class SSLFactory {
    /**
     * 创建SSLSocketFactory
     *
     * @param trustManager
     * @return
     */
    public static SSLSocketFactory build(X509TrustManager trustManager) {
        try {
            SSLContext sslContext = SSLContext.getInstance("TLS");
            sslContext.init(null, new TrustManager[]{trustManager}, new SecureRandom());
            return sslContext.getSocketFactory();
        } catch (NoSuchAlgorithmException e3) {
        } catch (KeyManagementException e5) {
        }
        return null;
    }

    /**
     * 创建SSLSocketFactory(双向认证)
     *
     * @param bks          jks转化之后的bks格式证书(转化方式: https://sourceforge.net/projects/portecle/files/latest/download?source=files下载portecle-1.9.zip)
     * @param pwd          证书的秘钥
     * @param trustManager
     * @return
     */
    public static SSLSocketFactory build(InputStream bks, String pwd, TrustManager trustManager) {
        try {
            SSLContext sslContext = SSLContext.getInstance("TLS");
            sslContext.init(buildClient(bks, pwd), new TrustManager[]{trustManager}, new SecureRandom());
            return sslContext.getSocketFactory();
        } catch (NoSuchAlgorithmException e3) {
        } catch (KeyManagementException e5) {
        }
        return null;
    }

    /**
     * 创建X509TrustManager
     *
     * @param inputStreams 包含公钥的cer证书
     * @return
     * @throws CertificateException
     * @throws NoSuchAlgorithmException
     * @throws KeyStoreException
     * @throws IOException
     */
    public static X509TrustManager getX509TrustManager(InputStream... inputStreams) throws CertificateException, NoSuchAlgorithmException, KeyStoreException, IOException {
        KeyStore keyStore = buildKeyStore(inputStreams);
        TrustManagerFactory tmf = TrustManagerFactory.getInstance(TrustManagerFactory.getDefaultAlgorithm());
        tmf.init(keyStore);
        TrustManager[] trustManagers = tmf.getTrustManagers();
        if (trustManagers.length != 1 || !(trustManagers[0] instanceof X509TrustManager)) {
            throw new IllegalStateException("Unexpected default trust managers:"
                    + Arrays.toString(trustManagers));
        }
        return (X509TrustManager) trustManagers[0];
    }

    private static KeyManager[] buildClient(InputStream bks, String pwd) {
        try {
            KeyStore clientKeyStore = KeyStore.getInstance(KeyStore.getDefaultType());
            // jks证书需要转化为bks格式
            clientKeyStore.load(bks, pwd.toCharArray());
            KeyManagerFactory keyManagerFactory = KeyManagerFactory.getInstance(KeyManagerFactory.getDefaultAlgorithm());
            keyManagerFactory.init(clientKeyStore, pwd.toCharArray());
            return keyManagerFactory.getKeyManagers();
        } catch (KeyStoreException e) {
            e.printStackTrace();
        } catch (CertificateException e) {
            e.printStackTrace();
        } catch (UnrecoverableKeyException e) {
            e.printStackTrace();
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }

    /**
     * 创建SSLSocketFactory(信任所有https)
     *
     * @return
     */
    @SuppressWarnings("强烈不建议使用, https形同虚设")
    public static SSLSocketFactory build() {
        SSLContext sslContext = null;
        try {
            sslContext = SSLContext.getInstance("TLS");
            sslContext.init(null, new TrustManager[]{new TrustAnyTrustManager()}, new SecureRandom());
        } catch (NoSuchAlgorithmException e1) {
        } catch (KeyManagementException e2) {
        }
        return sslContext.getSocketFactory();
    }

    /**
     * 创建KeyStore
     *
     * @param inputStreams
     * @return
     * @throws KeyStoreException
     * @throws CertificateException
     * @throws NoSuchAlgorithmException
     * @throws IOException
     */
    private static KeyStore buildKeyStore(InputStream... inputStreams) throws KeyStoreException, CertificateException, NoSuchAlgorithmException, IOException {
        String keyStoreType = KeyStore.getDefaultType();
        KeyStore keyStore = KeyStore.getInstance(keyStoreType);
        keyStore.load(null, null);
        List<Certificate> cas = readCert(inputStreams);
        for (int i = 0; cas != null && i < cas.size(); i++) {
            keyStore.setCertificateEntry(Integer.toString(i), cas.get(i));
        }
        return keyStore;
    }

    /**
     * 创建Certificate
     *
     * @param inputStreams
     * @return
     */
    private static List<Certificate> readCert(InputStream... inputStreams) throws CertificateException, IOException {
        List<Certificate> cas = new ArrayList<>();
        CertificateFactory cf = CertificateFactory.getInstance("X.509");
        for (InputStream is : inputStreams) {
            Certificate ca = cf.generateCertificate(is);
            is.close();
            cas.add(ca);
        }
        return cas;
    }

    /**
     * 信任所有https
     */
    private static class TrustAnyTrustManager implements X509TrustManager {

        public void checkClientTrusted(X509Certificate[] chain, String authType) throws CertificateException {
        }

        public void checkServerTrusted(X509Certificate[] chain, String authType) throws CertificateException {
        }

        public X509Certificate[] getAcceptedIssuers() {
            return new X509Certificate[]{};
        }
    }
}
```

在.logic里，获取接口 调用ui.activity的内容

在这个.net里，多是调用接口的方法，核心就是OKHTTP