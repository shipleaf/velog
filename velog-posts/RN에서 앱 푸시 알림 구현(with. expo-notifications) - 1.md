<h3 id="📌-rn-managed-flow에서-앱-푸시-알림-구현하기with-expo-notifications">📌 RN managed flow에서 앱 푸시 알림 구현하기(with. expo-notifications)</h3>
<p>현재 진행중인 프로젝트에서 앱 푸시 알림을 맡아 개발을 진행하게 되었다. 따라서, 관련 내용을 조사하고 문서로 남기기 위해 글을 작성한다.</p>
<hr />

<h3 id="📝-목차">📝 목차</h3>
<p>1️⃣ 기능 정의
2️⃣    구현 과정 설명
3️⃣ 샘플 테스트
4️⃣ 마무리</p>
<hr />

<h3 id="⚙️-기능-정의">⚙️ 기능 정의</h3>
<p>먼저, 우리 서비스는 React Native를 Expo managed flow와 함께 사용하며, Webview를 통해 서비스 화면을 만든다.</p>
<p>여러 종류의 알림이 필요할 것으로 예상되는데 정리해보면,</p>
<ol>
<li>사용자가 우리 서비스를 이용하기 시작할 때(시작 알림)</li>
<li>사용자가 우리 서비스 이용을 종료 및 결제했을 때(종료 알림)</li>
<li>사용자가 우리 서비스의 예약 기능을 사용했을 때(예약 확인 알림)</li>
</ol>
<p>이 중에서 우선 시작 및 종료 알림만 구현을 해보려 한다.</p>
<hr />

<h3 id="⚙️-구현-과정-설명">⚙️ 구현 과정 설명</h3>
<p>푸시 알림 과정을 간단하게 정리하면,</p>
<ol>
<li>앱 초기 실행 후 로그인 시 푸시 토큰 등록(알림 허용 등록)</li>
<li>앱에서 Expo 푸시 알림 토큰을 받아와서 서버로 전송</li>
<li>사용자가 서비스 이용 시작시 서버 이벤트 발생</li>
<li>서버에서 사용자별 저장된 푸시 토큰을 이용해 Expo 서버에 푸시 요청</li>
<li>Expo 서버가 해당 사용자에게 푸시 알림 전송</li>
<li>앱이 푸시 알림을 받아서 처리</li>
</ol>
<p>이렇게 정리할 수 있다. 여기서 Expo 서버는 Expo Push Notification Server로, android, ios로 푸시 알림을 보내주는 서버를 뜻한다. 푸시 알림은 크게 '로컬 알림'과 '서버 알림'으로 나뉘는데, 트리거의 주체가 어디냐에 따라 나뉘는 것으로 이번 프로젝트에서는 서버 알림을 다룬다.</p>
<h3 id="1-앱-초기-실행-후-로그인-시-푸시-토큰-등록알림-허용-등록">1. 앱 초기 실행 후 로그인 시 푸시 토큰 등록(알림 허용 등록)</h3>
<p>먼저, expo-notifications 모듈을 설치한다.</p>
<pre><code>npx expo install expo-notifications</code></pre><br />

<p>Expo 공식 문서에 expo-notifications의 사용법에 대한 코드가 있다. 코드를 서비스에 적용해보기 전에 분석 후 이해를 해보자!!(주석에도 설명을 달아두었다.)
<br /></p>
<pre><code class="language-js">import { useState, useEffect, useRef } from 'react';
import { Text, View, Button, Platform } from 'react-native';
import * as Device from 'expo-device';
import * as Notifications from 'expo-notifications';
import Constants from 'expo-constants';

Notifications.setNotificationHandler({
  handleNotification: async () =&gt; ({
    shouldShowAlert: true,
    shouldPlaySound: false,
    shouldSetBadge: false,
  }),
});

export default function App() {
  const [expoPushToken, setExpoPushToken] = useState('');
  const [channels, setChannels] = useState&lt;Notifications.NotificationChannel[]&gt;([]);
  const [notification, setNotification] = useState&lt;Notifications.Notification | undefined&gt;(
    undefined
  );
  const notificationListener = useRef&lt;Notifications.EventSubscription&gt;();
  const responseListener = useRef&lt;Notifications.EventSubscription&gt;();

  useEffect(() =&gt; {
    registerForPushNotificationsAsync().then(token =&gt; token &amp;&amp; setExpoPushToken(token));

    if (Platform.OS === 'android') {
      Notifications.getNotificationChannelsAsync().then(value =&gt; setChannels(value ?? []));
    }
    notificationListener.current = Notifications.addNotificationReceivedListener(notification =&gt; {
      setNotification(notification);
    });

    responseListener.current = Notifications.addNotificationResponseReceivedListener(response =&gt; {
      console.log(response);
    });

    return () =&gt; {
      notificationListener.current &amp;&amp;
        Notifications.removeNotificationSubscription(notificationListener.current);
      responseListener.current &amp;&amp;
        Notifications.removeNotificationSubscription(responseListener.current);
    };
  }, []);

  return (
    &lt;View
      style={{
        flex: 1,
        alignItems: 'center',
        justifyContent: 'space-around',
      }}&gt;
      &lt;Text&gt;Your expo push token: {expoPushToken}&lt;/Text&gt;
      &lt;Text&gt;{`Channels: ${JSON.stringify(
        channels.map(c =&gt; c.id),
        null,
        2
      )}`}&lt;/Text&gt;
      &lt;View style={{ alignItems: 'center', justifyContent: 'center' }}&gt;
        &lt;Text&gt;Title: {notification &amp;&amp; notification.request.content.title} &lt;/Text&gt;
        &lt;Text&gt;Body: {notification &amp;&amp; notification.request.content.body}&lt;/Text&gt;
        &lt;Text&gt;Data: {notification &amp;&amp; JSON.stringify(notification.request.content.data)}&lt;/Text&gt;
      &lt;/View&gt;
      &lt;Button
        title=&quot;Press to schedule a notification&quot;
        onPress={async () =&gt; {
          await schedulePushNotification();
        }}
      /&gt;
    &lt;/View&gt;
  );
}

async function schedulePushNotification() {
  await Notifications.scheduleNotificationAsync({
    content: {
      title: &quot;You've got mail! 📬&quot;,
      body: 'Here is the notification body',
      data: { data: 'goes here', test: { test1: 'more data' } },
    },
    trigger: {
      type: Notifications.SchedulableTriggerInputTypes.TIME_INTERVAL,
      seconds: 2,
    },
  });
}

async function registerForPushNotificationsAsync() {
  let token;

  if (Platform.OS === 'android') {
    await Notifications.setNotificationChannelAsync('myNotificationChannel', {
      name: 'A channel is needed for the permissions prompt to appear',
      importance: Notifications.AndroidImportance.MAX,
      vibrationPattern: [0, 250, 250, 250],
      lightColor: '#FF231F7C',
    });
  }

  if (Device.isDevice) {
    const { status: existingStatus } = await Notifications.getPermissionsAsync();
    let finalStatus = existingStatus;
    if (existingStatus !== 'granted') {
      const { status } = await Notifications.requestPermissionsAsync();
      finalStatus = status;
    }
    if (finalStatus !== 'granted') {
      alert('Failed to get push token for push notification!');
      return;
    }
    // EAS projectId is used here.
    try {
      const projectId =
        Constants?.expoConfig?.extra?.eas?.projectId ?? Constants?.easConfig?.projectId;
      if (!projectId) {
        throw new Error('Project ID not found');
      }
      token = (
        await Notifications.getExpoPushTokenAsync({
          projectId,
        })
      ).data;
      console.log(token);
    } catch (e) {
      token = `${e}`;
    }
  } else {
    alert('Must use physical device for Push Notifications');
  }

  return token;
}</code></pre>
<br />

<h4 id="1">(1)</h4>
<pre><code class="language-js">Notifications.setNotificationHandler({
  handleNotification: async () =&gt; ({
    shouldShowAlert: true, // 알림창 띄우기
    shouldPlaySound: false, // 알림음 재생
    shouldSetBadge: false, // 앱 뱃지 적용
  }),
});</code></pre>
<br />
=>
앱이 포그라운드(켜져 있을 때)에서 알림을 받을 때 처리하는 방식에 대한 함수이다.
정의를 해두지 않으면 푸시 알림시 UI에 아무것도 표시되지 않는다고 한다. 필요에 따라 유저가 설정을 변경할 수 있도록 할 수 있다.



<h4 id="2">(2)</h4>
<p>다음은 앱 푸시 알림 권한을 부여받기 위해 실행하는 함수이다. 코드가 너무 길어 잘라서 설명하려고 한다.</p>
<pre><code class="language-js">async function registerForPushNotificationsAsync() {
  let token;

  if (Platform.OS === 'android') {
    await Notifications.setNotificationChannelAsync('myNotificationChannel', {
      name: 'A channel is needed for the permissions prompt to appear',
      importance: Notifications.AndroidImportance.MAX,
      vibrationPattern: [0, 250, 250, 250],
      lightColor: '#FF231F7C',
    });
  }</code></pre>
<br />
=>
안드로이드는 알림 채널을 등록해야 하는데, 각각의 알림 채널은 고유의 진동, 소리, 우선순위 등을 가지기 때문에 알림 사용 전에 등록해야 한다. 채널을 등록하지 않으면 권한 프롬프트가 뜨지 않는 경우도 있다고 한다. (안드로이드 8.0부터는 알림 채널을 따로 등록하지 않는다고 한다!!)

<br />

<pre><code class="language-js">if (Device.isDevice) {
    const { status: existingStatus } = await Notifications.getPermissionsAsync();
    let finalStatus = existingStatus;
    if (existingStatus !== 'granted') {
      const { status } = await Notifications.requestPermissionsAsync();
      finalStatus = status;
    }
    if (finalStatus !== 'granted') {
      alert('Failed to get push token for push notification!');
      return;
    }</code></pre>
<br />

<p>=&gt; 본격적으로 푸시 알림 권한을 요청하는 부분이다. expo-notifications는 공식 문서에도 표기되어있듯 시뮬레이터, 에뮬레이터의 테스트를 지원하지 않는다. 따라서 Device.isDevice를 사용하여 실물 디바이스에서만 허용하도록 처리해준다.</p>
<br />

<pre><code class="language-js">try {
      const projectId =
        Constants?.expoConfig?.extra?.eas?.projectId ?? // eas project Id 추출(app.json)
        Constants?.easConfig?.projectId;
      if (!projectId) {
        throw new Error(&quot;Project ID not found&quot;);
      }
      token = (
        await Notifications.getExpoPushTokenAsync({
          projectId,
        })
      ).data;
      console.log(token);
    } catch (e) {
      token = `${e}`;
    }
  } else {
    alert(&quot;Must use physical device for Push Notifications&quot;);
  }

  return token;
}</code></pre>
<br />
=>
Expo notifications 토큰을 발급받기 위해서는 현재 프로젝트의 eas projectId가 필요하다. 각자 RN 프로젝트 app.json 파일 eas 블럭에 projectId가 표기되어있다.

<p>이 projectId를 추출하여 발급받은 token 값을 return하는 함수이다.</p>
<br />

<h4 id="3">(3)</h4>
<pre><code class="language-js">async function schedulePushNotification() {
  await Notifications.scheduleNotificationAsync({
    content: {
      title: &quot;You've got mail! 📬&quot;,
      body: 'Here is the notification body',
      data: { data: 'goes here', test: { test1: 'more data' } },
    },
    trigger: {
      type: Notifications.SchedulableTriggerInputTypes.TIME_INTERVAL,
      seconds: 2,
    },
  });
}</code></pre>
<br />

<p>=&gt; 알림의 내용과 트리거를 정의하는 부분이다. 알림 content의 data 부분은 푸시 알림을 눌렀을 때 앱 페이지 어디로 이동하는지 등을 정의할 수 있다.</p>
<pre><code>예시)
data : { url : &quot;/mainpage&quot; }</code></pre><p>트리거(trigger) 부분은 언제 알림을 보낼지 설정하는 기능인데, 우리 서비스에서는 이 트리거를 서버에서 작동하도록 설정해야 한다. 예문에서는 time_interval을 사용해 2초 뒤에 알림이 가도록 설정되어 있다.</p>
<br />

<h4 id="4">(4)</h4>
<pre><code class="language-js">useEffect(() =&gt; {
    registerForPushNotificationsAsync().then(token =&gt; token &amp;&amp; setExpoPushToken(token));

  // (1)
    if (Platform.OS === 'android') {
      Notifications.getNotificationChannelsAsync().then(value =&gt; setChannels(value ?? []));
    }

  // (2)
    notificationListener.current = Notifications.addNotificationReceivedListener(notification =&gt; {
      setNotification(notification);
    });

  // (3)
    responseListener.current = Notifications.addNotificationResponseReceivedListener(response =&gt; {
      console.log(response);
    });

    return () =&gt; {
      notificationListener.current &amp;&amp;
        Notifications.removeNotificationSubscription(notificationListener.current);
      responseListener.current &amp;&amp;
        Notifications.removeNotificationSubscription(responseListener.current);
    };
  }, []);
</code></pre>
<br />

<p>=&gt; 앱 실행 시, 위에서 정의한 함수들을 이용해 권한을 확인하고 토큰을 저장한다. (1)번 함수는 현재 안드로이드 디바이스에 등록된 채널을 가져오는 역할을 하며, (2)번 함수는 알림 수신 리스너를 등록하고, (3)번 함수는 알림 응답 리스너(수신한 알림 클릭 시 작동)를 등록하는 역할을 한다.</p>
<h3 id="샘플-테스트와-프로젝트-적용은-다음-포스트에서">샘플 테스트와 프로젝트 적용은 다음 포스트에서...</h3>