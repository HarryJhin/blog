# 안드로이드 권한 개요

앱 권한은 사용자의 데이터에 대한 접근으로부터 보호하기 위해 존재합니다.

## 앱 권한 선언

권한을 요청하는 프로세스는 권한 유형에 따라 달라집니다.

- 일반 권한 또는 서명 권한과 같은 설치 시간 권한인 경우에는 설치 시 자동으로 권한이 부여됩니다.
- 권한이 런타임 권한이며 앱이 Android 6.0(API Level 23) 이상을 실행하는 기기에서 설치된 경우 직접 권한을 요청해야 합니다.

???+ warning

    **주의**: 앱의 매니페스트에 선언하는 권한을 신중하게 고려해야 합니다. 앱에서 요청하는 각 권한의 경우 사용자에게 이득이 있어야 하며 사용자에게 명확한 방식으로 실행되어야 합니다.

### 매니페스트에 선언

앱이 요청할 수 있는 권한을 선언하려면 매니페스트에 적절한 `<uses-permissions>` 요소를 추가해야 합니다.

예를 들어, 카메라에 접근하는 앱에는 `AndroidMenifest.xml`에 다음 줄이 있습니다.

``` xml title="AndroidMenifest.xml" hl_lines="2"
<manifest ...>
    <uses-permission android:name="android.permission.CAMERA"/>
    <application ...>
        ...
    </application>
</manifest>
```

### 선택사항으로 선언

일부 안드로이드 기기에서는 카메라와 같은 일부 하드웨어가 존재하지 않을 수 있습니다. 앱에서 이런 하드웨어 관련 관한을 선언하는 경우, 항상 정상적으로 작동할 수 있도록 고려해야 합니다. 따라서 매니페스트 파일의 `<uses-feature>` 선언에서 `android:required`를 `false`로 설정하여 선택사항으로 선언하는 것이 좋습니다.

``` xml title="AndroidMenifest.xml" hl_lines="6 7"
<manifest ...>
    <uses-permission android:name="android.permission.CAMERA"/>
    <application>
        ...
    </application>
    <uses-feature android:name="android.hardware.camera"
                  android:required="false" />
<manifest>
```

???+ warning

    **주의**: 만약 이렇게 설정하지 않았을 경우 앱이 실행되려면 하드웨어가 필요하다고 가정하고 안드로이드 시스템에서 설치 자체를 하지 못하게 막을 수 있습니다.
