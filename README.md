# Native ads for Unity
Tool native ads for Unity

## Adding the SDK
### 1. Add the Google Mobile Ads plugin to your project <br>
- [Download](https://github.com/googleads/googleads-mobile-unity/releases) and import Google Mobile Ads plugin
### 2. Add the GoogleMobileAds-native and ToolNativeAd to your project <br>
- [Download](https://github.com/unity-package/native-ads-unity/releases) and import  GoogleMobileAds-native and ToolNativeAd sdk

### 3. Force resolve dependencies
Force resolve the dependencies from Assets/External Dependency Manager/Android Resolver/Force Resolve if the resolver did not open automatically.

## Setup Id

### 1. Add AdMob app ID

- You can open this from Assets/Google Mobile Ads/Settings

![image](https://github.com/user-attachments/assets/9e82b1c8-ae6b-4fc8-ac94-7f263ee8a5b5)

- Add the AdMob application IDs here


![image](https://github.com/user-attachments/assets/e563636b-3eac-45e4-a301-e14c77961648)

### 2. Add NativeAd ID

- Via `Tools -> NativeAd Settings` to open NativeAdSettings Window

![Screenshot 2024-11-29 102331](https://github.com/user-attachments/assets/2ceeb3fc-9f47-421a-88b5-762f6a0b5f23)

- Add Native Ads Ids here

![Screenshot 2024-11-29 102336](https://github.com/user-attachments/assets/b4615a5a-b5d9-44ce-87bc-7ee5b78c5ed6)

- `Use TestMode` equals `true`, you will use the Google Mobile Ads test Id

## Scene setup

### 1. Drag and Drop `NativeAdHolderTemplate` prefab 

- Drag and drop any of the Native ad unit prefab from the path `Assets > ToolNativeAd > Prefabs > NativeAdHolderTemplate` into your gameplay scene.


![Screenshot 2024-11-29 102217](https://github.com/user-attachments/assets/35cad516-b98c-45f5-90cd-fc193018ea71)

  
![Screenshot 2024-11-29 102239](https://github.com/user-attachments/assets/239cc680-1d8d-4c7b-aa65-6961851f0639)


![Screenshot 2024-11-29 102248](https://github.com/user-attachments/assets/40bb07d7-85fb-4bb3-8bf7-fa9f93221801)

### 2. Edit `NativeAdHolderTemplate`

- Edit the size, layout and image PlaceHolder in NativeAdHolder to suit your needs

(Note: When the ad fails to load, PlaceHolder will display)


## Handle Script

### 1. FetchAd, Adtive and Block

```csharp
        public NativeAdHolder nativeAdHolder;

        /// <summary>
        ///  Fetch and show Native Ad
        /// </summary>
        public void FetchAd()
        {
            nativeAdHolder.FetchAd();
        }

        /// <summary>
        /// Hide visual NativeAd and show PlaceHolder
        /// </summary>
        public void BlockAd()
        {
            nativeAdHolder.Block();
        }

        /// <summary>
        /// Show visual NativeAd and hide PlaceHolder
        /// </summary>
        public void ActiveAd()
        {
            nativeAdHolder.Active();
        }
```

Note: In some cases the click goes through the popup and triggers the NativeAd, call the `Block` method to prevent this. The `Active` method is the opposite of `Block`

### 2. Tracking revenue

```csharp
        public NativeAdHolder nativeAdHolder;
        
        private void OnEnable()
        {
            nativeAdHolder.Event_OnAdPaid += OnAdPaid;
        }

        private void OnDisable()
        {
            nativeAdHolder.Event_OnAdPaid -= OnAdPaid;
        }

        private void OnAdPaid(AdValue adValue)
        {
            Debug.Log(adValue.CurrencyCode);
            Debug.Log(adValue.Value);
        }
```
- Use the `Event OnAdPaid` event to register a callback to perform tracking
