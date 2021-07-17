+ activity_home_pager.xml(开始页面)

+ activity_patient_info_query_mirror_new.xml(查看历史报告)

+ activity_setting2.xml(设置)【关闭语音，在线更新，当前版本，退出登录】

  ↓ 点了start

+ activity_phone.xml(输入手机号界面)

  ↓ 点了【继续】

+ activity_zhi_qing_tong_yi_shu.xml（知情同意书界面）【手写签字，SignatureView】

  ↓ 签完字点了【继续】

+ activity_ge_ren_xin_xi2.xml(个人信息选择页面)【点按钮、显示隐藏按钮】

  ↓ 点了【继续】

+ activity_shen_gao.xml(选择身高页面)【竖版刻度尺】ScaleView_vertical.默认值135

  ↓ 点了【继续】

+ activity_ti_zhong.xml(选择体重页面)【竖版刻度尺】默认值50

  ↓ 点了【开始诊断】

+ activity_take_photo.xml(舌象检测开始页面)

  + ↓ 点【下一步】         
    + activity_record_video.xml【其中舌面通过变量select_type(0/1)来确定】  
  + ↓ 点【跳过本次检测】
    + activity_take_face_photo.xml(面象检测开始页面)
  + ↓ 点【退出当前检测】
    + 跳温馨提示

  ↓ 点【下一步】

+ activity_case_history.xml【既往病史选择页面】

  + 在CaseHistoryActivity.java中隐藏了
  + 在ids.xml中有item的name、type（包括33道测试题）

  ↓

+ activity_corporeity_check.xml选一道题就生成一个testMap

+ activity_patient_info_query_results_mirror_new.xml(体质检测结果页面)

+ activity_mian_xiang_result.xml(面诊结果页面)【其中写了假值来测试UI】

+ activity_she_zhen_result.xml(舌诊结果页面)

+ activity_jian_kang_fang_an.xml（查看健康方案页面）

