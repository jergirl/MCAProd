---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#모니터링 및 로깅
{: #monitoringandlogging}

*마지막 업데이트 날짜: 2016년 5월 24일*
{: .last-updated}

앱을 모니터링하고 로그를 검토하면서 애플리케이션 실행을 따라 가면 배치에 대해 더 잘 이해할 수 있습니다. 또한 문제를 찾아 이를 해결하는 데 드는 시간과 노력을 줄일 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix}} 애플리케이션은 넓게 배포되는 다중 인스턴스 애플리케이션으로, 애플리케이션의 실행과 이의 데이터를 다수의 서비스에서 공유할 수 있습니다. 이러한 복합 환경에서 앱을 모니터링하고 로그를 검토하는 것은 앱 관리에 중요합니다. 

##앱 모니터링 및 로깅
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}}에는 실행 중인 앱의 로그 파일을 생성하는 로깅 메커니즘이 기본 제공됩니다. 로그를 통해 사용자 앱에 대해 생성된 오류, 경고 및 정보 메시지를 확인할 수 있습니다. 또한 로그 메시지를 로그 파일에 기록하도록 앱을 구성할 수도 있습니다. 로그 형식 및 로그를 보는 방법에 대한 자세한 정보는 [Cloud Foundry에서 실행 중인 앱 로깅](#logging_for_bluemix_apps)을 참조하십시오.

앱을 모니터링하면 앱 개발을 보고 제어할 수 있습니다. 모니터링을 사용하여 다음 태스크를 수행할 수 있습니다.

* 앱 인스턴스의 성능 정보를 수집 및 모니터링하고 이들이 작동 가능한지 확인합니다. 
* 잠재적 병목 현상 발견 또는 업그레이드가 필요한 시점 등과 같이 애플리케이션 운영에 대한 통찰력을 얻습니다. 
* 자원 사용량 및 비용을 예측합니다. 

{{site.data.keyword.Bluemix_notm}} 플랫폼에서 사용자의 배치를 안정적으로 운용하기 위해서는 문제점을 즉각 발견하여 원인을 효율적으로 판별하는 것이 좋습니다. 이를 위해서는 문제점 해결을 염두에 두고 앱을 개발하며 {{site.data.keyword.Bluemix_notm}}에 앱을 배치할 때 모니터링과 로깅을 위한 서비스나 도구를 사용하십시오. 

###Cloud Foundry에서 실행되는 앱 모니터링
{: #monitoring_bluemix_apps}

Cloud Foundry 인프라를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 앱을 실행하는 경우 작동 상태, 자원 사용량, 트래픽 메트릭 등 성능 정보를 받아보기를 원합니다. 이러한 성능 정보가 있으면 그에 맞게 의사 결정을 하거나 조치를 취할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}} 앱을 모니터하려면 다음 방법 중 하나를 사용하십시오.

* {{site.data.keyword.Bluemix_notm}} 서비스. 모니터링 및 분석은 애플리케이션 성능을 모니터링할 때 사용할 수 있는 서비스를 제공합니다. 또한 이 서비스는 로그 분석과 같은 분석 기능도 제공합니다. 자세한 정보는 [Monitoring and Analytics](../services/monana/index.html)를 참조하십시오. 
* 써드파티 옵션. 예를 들어, [New Relic](http://newrelic.com/){:new_window}이 있습니다. 

###Cloud Foundry에서 실행되는 앱 로깅
{: #logging_for_bluemix_apps}

로그 파일은 Cloud Foundry 인프라를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 앱을 실행할 때 자동으로 작성됩니다. 배치에서 런타임까지 어느 단계에서 오류가 발생하더라도 로그를 확인하여 문제를 해결하는 데 도움이 되는 단서를 얻을 수 있습니다.

<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



###로그 형식
{: #log_format}

{{site.data.keyword.Bluemix_notm}} 애플리케이션에 대한 로그는 다음 패턴과 유사하게 고정 형식으로 표시됩니다. 

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

모든 로그 항목에는 네 개의 필드가 포함됩니다. 각 필드에 대한 간략한 설명은 다음 목록을 참조하십시오. 

<dl>
<dt><strong>시간소인</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>열: 1 - 27</p>
<p>로그 명령문의 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다. </p>
</dd>

<dt><strong>컴포넌트</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>열: 29 - 40</p>
<p>로그를 생성하는 컴포넌트. 다음 목록에 모든 컴포넌트에 대한 정의가 제공됩니다. </p>

<dl>
<dt><strong>APP</strong></dt>
<dd>애플리케이션. 컴포넌트 APP 뒤에는 슬래시와 애플리케이션 인스턴스를 표시하는 숫자가 후속합니다. 0이 첫 번째 인스턴스인 경우 1이 두 번째가 되는 등입니다. </dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API</dd>

<dt><strong>DEA</strong></dt>
<dd>DEA(Droplet Execution Agent)</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator</dd>

<dt><strong>RTR</strong></dt>
<dd>라우터</dd>

<dt><strong>STG</strong></dt>
<dd>스테이징</dd>
</dl>
</dd>

<dt><strong>스트림</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>열: 42 - 44</p>
<p>로그 메시지가 기록되는 스트림. <samp class="ph codeph">OUT</samp>은 <samp class="ph codeph">stdout</samp> 스트림을 나타내고 <samp class="ph codeph">ERR</samp>은 <samp class="ph codeph">stderr</samp> 스트림을 나타냅니다. </p>
</dd>

<dt><strong>메시지</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>열: 46 - 행의 끝</p>
<p>컴포넌트에서 발행하는 메시지. 메시지는 컨텍스트에 따라 달라집니다.</p>
</dd>

</dl>

###로그 보기
{: #viewing_logs}

세 위치에서 Cloud Foundry 앱에 대한 로그를 볼 수 있습니다.

  * [{{site.data.keyword.Bluemix_notm}} Dashboard](#viewing_logs_UI){:new_window}
  * [명령행 인터페이스](#viewing_logs_cli){:new_window}
  * [외부 로그 호스트](#thirdparty_logging){:new_window}

#### {{site.data.keyword.Bluemix_notm}} 대시보드에서 로그 보기
{: #viewing_logs_UI}

배치 또는 런타임 로그를 보려면 다음 단계를 완료하십시오.
1. {{site.data.keyword.Bluemix_notm}}에 로그인한 다음 대시보드에서 사용자의 앱에 대한 타일을 클릭하십시오. 앱 세부사항 페이지가 표시됩니다.
2. 왼쪽 탐색줄에서 **로그**를 클릭하십시오.

**로그** 콘솔에서 앱에 대한 최신 로그 또는 실시간 비상 로그를 볼 수 있습니다. 또한 로그 유형 및 채널별로 로그를 필터링할 수 있습니다.

**참고:** 로그는 앱 충돌 및 배치 사이에서 지속되지 않습니다.



#### 명령행 인터페이스에서 로그 보기
{: #viewing_logs_cli}

명령행 인터페이스를 통해 로그를 보려면 다음 옵션 중에서 선택하십시오. 

<ul>
<li>앱 배치 시 로그 추적
<p>**cf logs** 명령을 사용하여 {{site.data.keyword.Bluemix_notm}}에 앱을 배치할 때 앱과 상호작용하는 시스템 컴포넌트 및 앱에서 로그를 표시합니다. cf 명령행 인터페이스에 다음 명령을 입력할 수 있습니다. cf 로그에 대한 자세한 정보는 <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target="_blank">Log Types and Their Messages in Cloud Foundry</a>를 참조하십시오.</p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>가장 최신의 로그를 표시합니다. </dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>이 명령을 실행한 시점부터 생성된 로그를
표시합니다. </dd>
</dl>
<div class="note tip"><span class="tiptitle">팁:</span> 명령행 창에 <span class="keyword cmdname">cf push</span> 또는
<span class="keyword cmdname">cf start</span> 명령을 실행하는 경우, 다른 명령행 창에 <samp class="ph codeph">cf logs appname --recent</samp>를 입력하여
로그를 실시간으로 확인할 수 있습니다. </div>
</li>

<li>앱 배치 후 로그 보기
<p>애플리케이션 로깅이 사용되는 경우 런타임 시 앱에 문제가 발생하면 다음과 같은 애플리케이션 로그를 볼 수 있습니다. 애플리케이션 로그는 오류의 원인 판별에 도움이 됩니다. </p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>이 로그 파일은 디버깅을 위해 자세한 정보 이벤트를 기록합니다. 이 로그를 사용하여 빌드팩 실행 문제점을
해결할 수 있습니다. </p>
<p><span class="ph filepath">buildpack.log</span> 파일에 데이터를 생성하려면, 다음 명령을 입력하여 빌드팩 추적을 사용으로 설정해야 합니다.
   <pre class="pre">cf set-env <var class="keyword varname">appname</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>이 로그를 보려면 다음 명령을 입력하십시오.
<pre class="pre">cf files <var class="keyword varname">appname</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>이 로그 파일은 스테이징 태스크의 주요 단계 후 메시지를 기록합니다. 이 로그를 사용하여 스테이징 문제점을
해결할 수 있습니다. </p>
<p>이 로그를 보려면 다음 명령을 입력하십시오.
<pre class="pre">cf files <var class="keyword varname">appname</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**참고:** 애플리케이션 로깅 사용 방법에 대한 정보는 [런타임 오류 디버깅](../debug/index.html#debugging-runtime-errors)을 참조하십시오. 




###로그 필터링
{: #filtering_logs}

관심있는 로그를 보거나 보고 싶지 않은 컨텐츠를 제외하려면 cf 명령행 인터페이스에서 **cf logs** 명령을 필터링 옵션(예: **cut** 및 **grep**)과 함께 사용하십시오. 

* 전체적인 상세 로그 대신 일부분만 보려면 **cut** 옵션을 사용하십시오. 예를 들어, 컴포넌트 및 메시지 정보를 표시하려면 다음 명령을 사용하십시오.

```
cf logs appname --recent | cut -c 29-40,46- 
```

**grep** 옵션에 대한 자세한 정보를 보려면 cut --help를 입력하십시오. 
* 특정 키워드가 포함된 로그 항목을 표시하려면 **grep** 옵션을 사용하십시오. 예를 들어, [APP 키워드가 포함된 로그 항목을 표시하려면 다음 명령을 사용하십시오.

```
cf logs appname --recent | grep '\[App'
```
**grep** 옵션에 대한 자세한 정보를 보려면 `grep --help`를 입력하십시오.



### 외부 로그 호스트 구성
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}}는 메모리에 제한된 양의 로그 정보를 보관합니다. 정보가 로깅되면 이전 정보는 새 정보로 바뀝니다. 로그 정보를 모두 보관하려면 써드파티 로그 관리 서비스와 같은 외부 로그 호스트 또는 기타 호스트에 로그를 저장할 수 있습니다.

앱 및 시스템에서 외부 로그 호스트로 로그를 스트림하려면 다음 단계를 수행하십시오.

  1. 로깅 엔드포인트를 판별하십시오. 
     
	 Papertrail, Splunk 또는 Sumologic 등의 써드파티 로그 수집기에 로그를 전송할 수 있습니다. 또한 syslog 호스트, TLS(Transport Layer Security)로 암호화된 syslog 호스트 또는 HTTPS POST 엔드포인트에 로그를 전송할 수 있습니다. 로깅 엔드포인트를 얻기 위한 방법은 로그 호스트에 따라 다릅니다.

  2. 사용자 제공 서비스 인스턴스를 작성하십시오.
     
	 `'cf create-user-provided-service'` 명령 또는 `'cups'`(명령의 짧은 버전)를 사용하여 사용자 제공 서비스 인스턴스를 작성하십시오.
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 **service_name**
	 
	 사용자 제공 서비스 인스턴스의 이름입니다.
	 
	 **logging_endpoint**
	 
	 {{site.data.keyword.Bluemix_notm}}에서 로그를 전송하는 로깅 엔드포인트입니다. *logging_endpoint*를 사용자의 값으로 교체하려면 다음 표를 참조하십시오.
	 
	 <table>
     <thead>
     <tr>
     <th>로깅 엔드포인트</th>
     <th>명령</th>
	 <th>참고</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog 호스트</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>예를 들어, Papertrail에 로깅을 사용하려면 `cf cups my-logs -l syslog://<papertrail-url>`을 입력하십시오. `<papertrail-url>`을 Papertrail의 사용자 로깅 엔드포인트의 URL로 대체하십시오.</td>
     </tr>
	 <tr>
     <td>syslog-tls 호스트</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>인증서는 인증 기관에 의해 신뢰받아야 합니다. 자체 서명 인증서를 사용하지 마십시오.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>이 엔드포인트는 공용 인터넷에 있어야 하며 {{site.data.keyword.Bluemix_notm}}에 의해 액세스될 수 있어야 합니다.</td>
     </tr>
     </tbody>
     </table>	
  3. 서비스 인스턴스를 앱에 바인딩하십시오. 

	 다음 명령을 사용하여 서비스 인스턴스를 앱에 바인딩하십시오. 
	
	 ```
	 cf bind-service appname <service_name>
	```
	 **appname**
	 
	 앱의 이름입니다.
	 
	 **service_name**
	 
	 사용자 제공 서비스 인스턴스의 이름입니다.
	 
  4. 앱을 다시 스테이징하십시오.
     변경사항이 적용되도록 ```cf restage appname```을 입력하십시오. 

#### 외부 호스트에서 로그 보기
{: #viewing_logs_external}

	 
로그가 생성될 때 짧은 지연 후에 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스 또는 cf 명령행 인터페이스에서 표시되는 메시지와 유사한 메시지를 외부 로그 호스트에서 볼 수 있습니다. 앱의 다중 인스턴스가 있는 경우, 로그가 집계되고 앱에 대한 모든 로그를 볼 수 있습니다. 또한 로그는 앱 충돌 및 배치 사이에서 지속됩니다.

**참고:** 명령행 인터페이스에 표시된 로그는 syslog 형식이 아니며 외부 로그 호스트에 표시된 메시지와 정확히 일치하지 않을 수 있습니다. 

### 예: Cloud Foundry 애플리케이션 로그를 Splunk에 스트리밍 
{: #splunk}

이 예에서, 이름이 Jane인 개발자는 IBM Virtual Servers Beta 및 Ubuntu 이미지를 사용하여 가상 서버를 작성합니다. Jane은 {{site.data.keyword.Bluemix_notm}}에서 Splunk로 Cloud Foundry 앱 로그의 스트리밍을 시도합니다.  

  1. 우선 Jane은 Splunk를 설정합니다. 

     a. Jane은 [Splunk Light 다운로드 사이트](https://www.splunk.com/en_us/download/splunk-light.html){:new_window}에서 Splunk Light를 다운로드한 후에 다음 명령을 사용하여 이를 설치합니다. 소프트웨어는 */opt/splunk*에 설치됩니다.  
       
	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```
	   
     b. Jane은 {{site.data.keyword.Bluemix_notm}}와의 통합을 위해 RFC5424 syslog 기술 추가 기능을 설치하고 패치합니다. 추가 기능 설치 관련 지시사항에 대한 자세한 정보는 [Cloud Foundry 가이드라인](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}을 참조하십시오.   

	    Jane은 다음 명령을 사용하여 추가 기능을 설치합니다. 
        
	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```
	   
        그리고 Jane은 */opt/splunk/etc/apps/rfc5424/default/transforms.conf*를 다음 텍스트로 구성된 새 *transforms.conf* 파일로 대체하여 추가 기능을 패치합니다. 
	   
	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}	   

     c. Splunk가 설정되면, Jane은 Ubuntu 시스템의 일부 포트를 열어서 수신 syslog 드레인(포트 5140) 및 Splunk 웹 UI(포트 8000)를 허용해야 합니다. {{site.data.keyword.Bluemix_notm}} 가상 서버에 방화벽이 기본적으로 설정되어 있기 때문입니다. 
	   
	    **참고:** iptable 구성은 Jane의 평가 용도로 여기서 수행되며, 이는 임시적입니다. 프로덕션에서 Bluemix 가상 서버의 방화벽 설정을 구성하려면, [네트워크 보안 그룹](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} 문서에서 세부사항을 참조하십시오. 
	 
	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}	
	  
	   그리고 Jane은 다음 명령을 사용하여 Splunk를 실행합니다. 

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```
		
  2. Jane은 {{site.data.keyword.Bluemix_notm}}에서 syslog 드레인을 허용하도록 Splunk 설정을 구성합니다. Jane은 syslog 드레인에 대한 데이터 입력을 작성해야 합니다. 

     a. Splunk 웹 인터페이스의 왼쪽에서 Jane은 **데이터 > 데이터 입력**을 클릭합니다. Splunk에서 지원하는 입력 유형의 목록이 표시됩니다.  
	 
     b. syslog 드레인이 TCP 프로토콜을 사용하므로, Jane은 **TCP**를 선택합니다. 
	 
     c. **TCP** 분할창에서, Jane은 **포트** 필드에 **5140**을 입력하고 나머지 필드는 공백으로 남겨둔 후에 **다음**을 클릭합니다. 
	 
     d. **소스 유형** 목록에서 Jane은 **미분류 > rfc5424_syslog**를 선택합니다. 
	 
     e. **메소드** 유형에 대해 Jane은 **IP**를 선택합니다. 
	 
     f. **색인** 필드에서 Jane은 **색인 새로 작성**을 클릭합니다. 그리고 새 색인의 이름을 "bluemix"로 지정한 후에 **저장**을 클릭합니다. 
	 
     g. 최종적으로 **검토** 창에서, Jane은 설정이 올바른지 확인한 후에 **제출**을 클릭하여 이 데이터 입력을 사용합니다. 

  3. {{site.data.keyword.Bluemix_notm}}에서, Jane은 syslog 드레인 서비스를 작성하고 이 서비스를 앱에 바인드합니다. 

     a. Jane은 cf cli에서 다음 명령을 사용하여 syslog 드레인 서비스를 작성합니다. 
	 
     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```
        
     **참고:** *dummyhost*는 실제 이름이 아닙니다. 이는 실제 호스트 이름을 숨기는 데 사용됩니다.  

     b. Jane은 syslog 드레인 서비스를 자체 영역의 앱에 바인드한 후에 앱을 다시 스테이징합니다. 
	 
	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```
		

Jane은 자신의 앱을 사용해 본 후에 Splunk 웹 인터페이스에서 다음의 조회 문자열을 입력합니다. 

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane은 Splunk 웹 인터페이스에서 로그의 스트림을 봅니다. 설치하는 Splunk가 Splunk Light이지만, Jane은 매일 500MB 로그를 계속 보유할 수 있습니다.  




