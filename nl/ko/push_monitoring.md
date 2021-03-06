---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 알림 모니터 
{: #push_monitoring}
마지막 업데이트 날짜: 2017년 10월 30일
{: .last-updated}


IBM {{site.data.keyword.mobilepushshort}} 서비스가 확장되어 이제 사용자 데이터에서 그래프를 생성하여 푸시 성능을 모니터할 수 있는 기능을 제공합니다. 유틸리티를 사용하여 일별, 주별 또는 월별 기준으로 전송된 푸시 알림을 모두 나열하거나 등록된 디바이스를 모두 나열하여 정보를 분석할 수 있습니다.

전송된 모든 알림에 대한 보고서를 생성하려면 [REST API](https://mobile.{DomainName}/imfpush/#!/messages/get_apps_applicationId_messages_report){: new_window}에 있는 푸시 메시지 GET 메소드를 사용하십시오. 
	![전송된 알림 보고서](images/monitoring_messages.jpg)


등록된 모든 디바이스에 관한 보고서를 생성하려면 [REST API](https://mobile.{DomainName}/imfpush/#!/devices/get_apps_applicationId_devices_report){: new_window}의 푸시 디바이스 등록 GET 보고서 메소드를 사용하십시오.
	![등록된 디바이스 보고서](images/monitoring_devices.jpg)


사용자의 플랫폼에 해당하는 모니터링 유틸리티 사용 방법에 대한 정보는 다음을 참조하십시오.

 - [Android 디바이스에서 푸시 알림 모니터링](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push/tree/Doc#monitoring).
 - [애플리케이션에서 푸시 알림 모니터링](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/Doc#enable-monitoring).

참고:

1. {{site.data.keyword.mobilepushshort}} 모니터링 탭에는 분석 데이터가 표시되지 않습니다. 
2. REST API를 사용하여 생성된 보고서는 캐시되며 캐시는 30분 간 유지됩니다.
또한 그래프에 표시되는 데이터는 캐시된 데이터로부터 생성됩니다. 
 



 
